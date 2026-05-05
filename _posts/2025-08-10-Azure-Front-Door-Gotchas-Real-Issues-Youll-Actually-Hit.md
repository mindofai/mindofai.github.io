---
published: true
layout: post
title: Azure Front Door Gotchas (Real Issues You’ll Actually Hit)
author: bryananthonygarcia
date: 2025-08-10 12:00
tags: [Azure, Front Door, Cloud, DevOps, Architecture, Troubleshooting]
---

# Azure Front Door Gotchas (Real Issues You’ll Actually Hit)

Azure Front Door is powerful. Once you get it working, it feels clean, scalable, and flexible.

But getting there? Not always smooth.

This blog is not about how Azure Front Door works. It’s about the real issues you’ll hit when you actually start using it in a real project. The stuff that doesn’t show up in documentation, but shows up immediately in production.

If you’re planning to use Azure Front Door for routing apps, APIs, or even WordPress, this will save you a lot of time.

## 1. CORS Issues That Don’t Make Sense

One of the first problems I ran into was CORS.

Everything worked fine locally. But once routed through Front Door, requests started failing.

The issue?

The backend (WordPress in my case) was still referencing its original domain instead of the Front Door domain.

For example:
- Backend URL: `staging.example-host.com`
- Front Door URL: `example.com`

The browser blocks this because the origins don’t match.

### Fix

- Make sure all assets and API calls use the Front Door domain  
- Avoid hardcoded URLs in your backend  
- Check your CMS configs (WordPress is a common culprit)  

![CORS Issue](./images/afd-cors.png)

## 2. Route Priority Breaking Everything

This one is very easy to miss.

If your routes are not ordered correctly, everything will still “work”… just not the way you expect.

For example:

- `/*`  
- `/api/*`  

If `/*` is above `/api/*`, then all API calls go to the wrong origin.

Azure Front Door matches the most specific route first, but ordering still matters in how you configure them.

### Fix

Always define routes from most specific to least specific:

1. `/api/*`  
2. `/login`  
3. `/home`  
4. `/*`  

![Route Priority](./images/afd-priority.png)

## 3. 404 Pages Acting Weird

You might notice this:

- Direct origin → proper styled 404 page  
- Through Front Door → plain or unexpected 404  

This happens because Front Door sometimes handles the request instead of forwarding it to the origin.

### Fix

- Ensure your fallback route is correctly configured  
- Make sure unmatched paths are still forwarded to your origin  
- Test both direct origin and Front Door behavior  

![404 Issue](./images/afd-404.png)

## 4. Headers Not Showing Where You Expect

At one point, I was sending a custom header:

`X-USER-AUTHENTICATED`

I could see it in the browser, but not in the backend.

That’s because:

- Response headers ≠ Request headers  
- What you see in DevTools is not always what your server receives  

### Fix

- Make sure you explicitly add headers as **request headers** in rule sets  
- Don’t rely on response headers for backend logic  

![Headers](./images/afd-headers.png)

## 5. WordPress (and Other CMS) Fighting Your Setup

If you're using something like WordPress behind Front Door, expect friction.

Common issues:
- Hardcoded URLs  
- Redirect loops  
- SEO metadata pointing to the wrong domain  
- Mixed content issues  

### Fix

- Update site URL settings  
- Check plugins (especially SEO plugins)  
- Avoid using staging URLs in production configs  

![WordPress Issue](./images/afd-wordpress.png)

## 6. Debugging Is Not Straightforward

Unlike local apps, debugging Front Door is not always obvious.

You’re dealing with:
- Edge routing  
- Multiple origins  
- Rule sets  
- Headers  

So when something breaks, it’s not always clear where the issue is.

### What Helps

- Use browser DevTools (Network tab)  
- Check response headers  
- Test routes individually  
- Temporarily simplify routing  

Sometimes the fastest way to debug is to remove complexity and build it back step by step.

![Debugging](./images/afd-debug.png)

## Key Takeaways

- Most issues come from misconfiguration, not Azure itself  
- Route order matters more than you think  
- Always validate domains and origins  
- Headers behave differently than expected  
- CMS platforms introduce extra complexity  

## Final Thoughts

Azure Front Door is one of those services that feels simple until you start combining features.

Routing, rule sets, headers, and origins all interact with each other, and small mistakes can cause big issues.

The good news is that once you hit these problems and understand them, everything becomes much easier.

If you’re setting this up for the first time, expect a bit of trial and error. That’s normal.

Just make sure you understand how things flow, and you’ll be in a good spot.

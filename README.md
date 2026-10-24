# cheap proxies for scraping: What Budget Options Actually Cost, and When a Credit-Based API Beats Per-GB Pricing

Anyone searching for cheap proxies for scraping usually has the same underlying question: how do I get my scraper past blocks without paying enterprise prices? The honest answer is that "cheap" depends entirely on your target sites. A raw proxy list at $1.39 per IP looks cheap until you spend a week building rotation logic and CAPTCHA handling. An all-in-one scraping API looks expensive at $49/month until you realize a single engineer-hour costs more than that.

This guide breaks down what budget scraping actually costs in both models, with current ScraperAPI pricing (the scraping API this article covers in depth), the credit math most reviews skip, and a comparison against cheaper per-GB proxy providers so you can match the tool to your workload instead of your wishlist.

> **Quick pick:** For most developers scraping standard e-commerce and search pages at moderate volume, ScraperAPI's **Hobby plan at $49/month** (100,000 credits, 20 concurrent threads) is the realistic entry point — and plain HTML pages cost just 1 credit each. If you want to verify the math yourself before spending anything, the 7-day trial gives you 5,000 free credits. **👉 Check ScraperAPI's current plans and start the free trial**

## What "cheap" actually means for scraping

The cheapest option is the one with the lowest cost per *successfully scraped page*, and that number has almost nothing to do with the headline price on a pricing page.

There are two billing models in this market. Raw proxy providers bill by bandwidth (per GB) or per IP, and you handle rotation, retries, headers, and CAPTchas yourself. Scraping APIs bill per request in credits, and the service handles all of that for you — proxies, JavaScript rendering, CAPTCHA solving, automatic retries.

The per-GB model wins on raw unit price. The credit model wins on engineering time. A review from mid-2026 put it well: raw residential proxies give you more control at lower per-request cost, but you're trading money for engineering time. If fighting proxy bans costs you even ten hours, a $49/month API that eliminates that work pays for itself.

So before comparing any prices, answer two questions: what are you scraping, and how much of it? The rest of this article works through both.

## ScraperAPI plans and pricing: the full list

ScraperAPI currently publishes seven paid plans plus a free plan, all billed per request (credits) rather than bandwidth. Annual billing takes 10% off every plan. Here is everything currently shown on the official pricing page:

| Plan | Monthly price | Annual (per month) | API credits | Concurrent threads | Link |
| --- | --- | --- | --- | --- | --- |
| Free | $0 | — | 1,000/month | 5 | [Start free](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Hobby | $49 | $44.10 | 100,000 | 20 | [Get Hobby](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Startup | $149 | $134.10 | 1,000,000 | 50 | [Get Startup](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Business | $299 | $269.10 | 3,000,000 | 100 | [Get Business](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Scaling | $475 | $427.50 | 5,000,000 | 200 | [Get Scaling](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Professional | $975 | $877.50 | 10,500,000 | 300 | [Get Professional](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Advanced | $1,975 | $1,777.50 | 21,500,000 | 500 | [Get Advanced](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Enterprise | Custom | Custom | 22,000,000+ | 500+ | [Contact sales](https://www.scraperapi.com/pricing?fp_ref=coupons) |

Every paid plan includes the same core feature set: JavaScript rendering, premium residential and mobile proxies, JSON auto-parsing, CAPTCHA and anti-bot handling, custom headers and sessions, automatic retries, unlimited bandwidth, and a 99.9% uptime guarantee. The plans differ in credits, concurrency, geotargeting depth, and analytics history — a detail that matters more than it sounds, which we'll get to.

At the plain-HTML rate, costs per thousand pages work out like this: Hobby runs about $0.49 per 1,000 pages, Startup about $0.15, and Business under $0.10. **👉 See all plan prices and credit rates on ScraperAPI's pricing page** if you want to check current numbers before they change.

## The credit multiplier nobody budgets for

Here is the single most important thing budget shoppers miss: a "standard page" costs 1 credit, but many of the pages you actually want cost far more.

ScraperAPI prices difficult domains individually because it builds custom bypass logic for them. The published rates: an Amazon page costs 5 credits. Google and Bing (including subdomains) cost 25. LinkedIn costs 30. Any site behind Cloudflare, Datadome, or PerimeterX adds 10 credits per request when the bypass kicks in. Turning on JavaScript rendering costs about 10 credits on top of the base rate, and routing through the premium or ultra-premium residential/mobile pools adds another 10–30 credits per request.

Run the numbers on a realistic job and the picture changes fast. One detailed 2026 review worked through it: scraping Amazon search results with JS rendering enabled, a 1,000,000-credit plan might only cover 40,000–100,000 actual pages — not a million. Their exact warning: *"Do the math on a job that needs render=true plus premium=true on a protected target, and a single successful scrape can cost 20-30x that headline number."*

Two practical defenses exist, and both are free:

1. **Use the Domain Cost Estimator** in the ScraperAPI dashboard to check the exact credit cost of any URL before you commit to a plan.
2. **Set `max_cost` per scrape** so no single request can blow past a credit limit you choose.

Independent testing backs up the value side of this equation: one developer logged a 99.0% success rate across 50,000+ requests against Google, Amazon, and Zillow, and another reported 95–99% success on most targets — with failed requests not costing credits. On plain targets, those numbers make the effective per-page cost very competitive. On hard targets, they don't. Know which side you're on first.

## How ScraperAPI compares to cheap proxy providers

If you're comfortable managing proxies yourself, per-GB providers are genuinely cheaper per request. Here's what budget providers were publishing as of mid-2026:

| Provider | Model | Published rate | Best for |
| --- | --- | --- | --- |
| Webshare | Per IP (datacenter) | from ~$0.03/IP/month at 100-IP volume | Static IPs, simple targets |
| Smartproxy (rotating DC) | Per GB | ~$0.50/GB | Fast, stable datacenter rotation |
| PacketStream | Per GB | $1/GB | Ultra-budget residential, US/EU focus |
| IPRoyal | Per GB | $1.75/GB residential (PAYG, doesn't expire) | Bursty workloads without monthly commitment |
| DataImpulse | Per GB | $3.60/GB (Starter) | Unified credits across proxy types |
| Oxylabs | Per user/month | from $30 | Enterprise-grade raw proxy access |
| Bright Data | Per user/month | from $499 | Full-scale data platform |

At $1.75/GB residential and roughly 500 KB per rendered page, that's about $0.88 per 1,000 pages before you write any code — cheaper than ScraperAPI's plain-HTML rate on paper, until you count the hours spent building rotation, retry, and CAPTCHA logic.

The fair framing: if your targets are simple static pages and you already have infrastructure, raw proxies from any of the providers above cost less. If your targets are JS-heavy, protected, or you'd rather ship features than maintain a proxy stack, ScraperAPI's credit model usually wins on total cost. Its structured data endpoints (Amazon, Google Search and Shopping, Walmart returning parsed JSON directly) also remove parser-maintenance work that raw proxies never cover.

## The hidden limits that decide whether a plan works

Several restrictions only surface in ScraperAPI's documentation and FAQ, and they change which plan you should buy:

- **Geotargeting is US/EU-only below Business.** Hobby and Startup can only target US and EU locations. Country-level targeting anywhere else requires Business ($299) or higher. If your targets are in other regions, the $49 and $149 plans don't apply to you.
- **Exceeding concurrency gets you a 429, not a queue.** Requests above your thread limit are rejected outright — no queuing, no extra charge. Hobby's 20 threads can bottleneck a time-sensitive price-monitoring job.
- **Credits don't roll over.** Spiky workloads — one big crawl per quarter — pay for idle months. If that's your pattern, a per-GB provider with non-expiring traffic (IPRoyal's PAYG model, for example) fits better.
- **No overage below Scaling.** On Hobby through Professional monthly plans, running out of credits pauses your scraping until renewal, unless you opt into auto-upgrade (which moves you to the next tier). Pay-as-you-go overage only exists on Scaling, Professional, Advanced, and Enterprise — and it's capped by a spending limit you set, not a pre-charged amount.
- **Sticky sessions last about an hour.** Session support keeps the same IP across a request sequence, but not across a day. Login-state scraping and ad verification need a different tool.
- **You can't pick specific IPs or ASNs.** You control country, session, and IP tier. If you need that granularity, you want raw proxies.
- **Analytics history shrinks on cheap plans.** Hobby and Startup only keep 30 days of dashboard analytics; Business and up get unlimited history.

That last group of details rarely shows up in listicles that just rank providers by price-per-GB — but any one of them can disqualify a plan that looked perfect in a comparison table.

## Free trial, free plan, and the refund policy

ScraperAPI's trial terms are unusually concrete. You get a 7-day trial with 5,000 API credits to test at real scale, plus a permanent free plan of 1,000 credits per month (capped at 5 concurrent connections) for small projects. Need more test credits? Support can grant additional ones.

The refund policy is the part worth remembering: **a 7-day no-questions-asked refund** if you're unhappy for any reason — you contact support and they process it. Cancellation is self-serve from the dashboard at any time, with no cancellation fee. Combined with the trial, this means you can validate success rates on your actual target sites before any money is truly committed. **👉 Start the 7-day trial with 5,000 free credits and test your real targets**

One caution from the reviews: the 1,000-credit free plan is enough to verify the API works on your targets, not to run anything production-shaped. Treat it as a testing budget.

## Who should skip ScraperAPI entirely

Honest budgets require an honest exclusion list. ScraperAPI is the wrong tool if any of these describe you:

- **You're scraping LinkedIn, Instagram, or heavily protected e-commerce at real volume.** The ultra-premium multipliers will make this cost more than a dedicated residential plan billed by bandwidth.
- **You need 500K+ requests daily.** Even the Business plan's millions of credits evaporate under JS rendering at that volume; self-managed proxies plus your own browser cluster cost meaningfully less at that scale.
- **Your targets are plain static HTML and you already handle rotation.** A scraping API is overkill when `requests` + a $5 datacenter proxy list already works.
- **Your real goal is managing multiple social accounts.** That's an account-management problem, and forcing a scraping API into that role ends badly.

There's no shame in any of these — it just means your "cheap" lives somewhere else in the market.

## FAQ

**Are cheap proxies good enough for web scraping?**
For simple, unprotected targets, yes — datacenter proxies from $0.50/GB or $0.03/IP handle plain HTML fine. For anything behind Cloudflare, Datadome, or heavy JavaScript, cheap proxies usually fail silently, and the money you save gets spent on engineering workarounds. The deciding factor is target difficulty, never the sticker price.

**How much does ScraperAPI cost per page?**
Between 1 credit and 75 credits per request depending on the site and options. Plain HTML pages cost 1 credit (about $0.15 per 1,000 pages on Startup). Amazon costs 5, Google and Bing 25, LinkedIn 30, and bypassing bot protection adds 10. Check any URL's exact cost with the Domain Cost Estimator in the dashboard before buying.

**Does ScraperAPI have a free trial?**
Yes — 7 days with 5,000 API credits, plus a permanent free plan of 1,000 credits per month with 5 concurrent connections. There's also a 7-day no-questions-asked refund if you pay and change your mind.

**What's cheaper than ScraperAPI?**
Raw proxy providers: Webshare from roughly $0.03 per datacenter IP, Smartproxy's rotating datacenter pool around $0.50/GB, PacketStream at $1/GB, and IPRoyal residential at $1.75/GB with non-expiring pay-as-you-go traffic. They're cheaper per request but require you to build and maintain rotation, retries, and CAPTCHA handling yourself.

## Which plan should you actually buy

Match the plan to your situation rather than to the "most popular" badge:

- **Testing or under 20,000 pages/month on standard sites** → start with the free plan and the 7-day trial. Upgrade only when the trial proves out on your real targets.
- **Solo developer, standard e-commerce/SEO targets, US/EU geotargeting is enough** → Hobby at $49/month, or Startup at $149 if you're near the 100,000-credit ceiling. Watch the Startup-to-Business step: if your workload lands within 10% of the 1M-credit limit, either add `max_cost` and trim rendering, or jump straight to Business — there's no overage below Scaling to absorb the gap.
- **Production scraping with international targets** → Business at $299/month, since country-level geotargeting outside US/EU starts here.
- **Heavy protected-site volume** → compare the credit math honestly against per-GB providers before committing; Scaling's pay-as-you-go overage helps, but raw proxies may still win.
- **22M+ credits per month** → the Advanced tier or a custom Enterprise quote.

One last check before you buy anything: run ten pages from your actual target list through the trial and multiply the credit costs out to your monthly volume. It takes five minutes and it's the difference between a plan that fits and one that surprises you on the second invoice. **👉 Compare every plan and credit rate on ScraperAPI's pricing page**

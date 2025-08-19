---
---
<script src="assets/js/sorttable.js"></script>

<details open>
<summary>
Why does this exist?
</summary>
The SSO Wall of Shame showed the problem: too many vendors lock SSO behind punitive “enterprise” paywalls, discouraging adoption of a critical security control. That naming-and-shaming has helped — public pressure has nudged several companies to make SSO more accessible.

But security shouldn’t just be about avoiding shame. It should also be about celebrating the companies that get it right.

The SSO Wall of Fame exists to highlight vendors who treat SSO as the baseline security feature it is — whether by including it in all paid plans, offering it at a fair add-on price, or keeping the gap between non-SSO and SSO tiers reasonable.

By shining a light on good practice, we aim to:

Encourage more vendors to follow suit,

Give buyers a way to reward responsible vendors with their business, and

Move the industry toward a future where secure by default is the norm, not the exception.

In short: shame works, but fame is better.
</details>

{% assign all = site.vendors | sort: "name" %}
{% assign vendors = "" | split: ',' %}
{% assign call_us = "" | split: ',' %}
{% for vendor in all %}
	{% if vendor.sso_pricing contains "Call" %}
		{% assign call_us = call_us | push: vendor %}
	{% else %}
		{% assign vendors = vendors | push: vendor %}
	{% endif %}
{% endfor %}

## The List

<table class="sortable">
<thead>
<tr><th>Vendor</th><th>Base Pricing</th><th>SSO Pricing</th><th>% Increase</th><th>Source</th><th>Date Updated</th></tr>
</thead>
<tbody>
{% for vendor in vendors %}
<tr>
<td markdown="span"><a href="{{ vendor.vendor_url }}">{{ vendor.name }}</a></td>
<td markdown="span">{{ vendor.base_pricing }}</td>
<td markdown="span">{{ vendor.sso_pricing }}</td>
<td markdown="span">{{ vendor.percent_increase }}</td>
<td>
{% for source in vendor.pricing_source %}
{% if forloop.first == false %}
&amp;
{% endif %}
<a href="{{ source }}">&#128279;</a>
{% endfor %}
{{ vendor.pricing_note }}</td>
<td>{{ vendor.updated_at }}</td>
</tr>
{% endfor %}
</tbody>
</table>

## The Other List ##
Some vendors simply do not list their pricing for SSO because the pricing is negotiated with an account manager. These vendors get their own table as we assume they apply a significant premium for SSO.

<table class="sortable">
<thead>
<tr><th>Vendor</th><th>Base Pricing</th><th>SSO Pricing</th><th>% Increase</th><th>Source</th><th>Date Updated</th></tr>
</thead>
<tbody>
{% for vendor in call_us %}
<tr>
<td markdown="span"><a href="{{ vendor.vendor_url }}">{{ vendor.name }}</a></td>
<td markdown="span">{{ vendor.base_pricing }}</td>
<td markdown="span">{{ vendor.sso_pricing }}</td>
<td markdown="span">{{ vendor.percent_increase }}</td>
<td>
{% for source in vendor.pricing_source %}
{% if forloop.first == false %}
&amp;
{% endif %}
<a href="{{ source }}">&#128279;</a>
{% endfor %}
{{ vendor.pricing_note }}</td>
<td>{{ vendor.updated_at }}</td>
</tr>
{% endfor %}
</tbody>
</table>

## FAQs

<details>
<summary>
This doesn't scale linearly for number of seats!
</summary>
Correct. Since we don't know who's reading the page, it's easiest to just assume a team with no volume discount.
</details>

<details>
<summary>
How is base pricing determined?
</summary>
We disregard free tier pricing, as we can assume these aren't intended for long term business customer use. We also disregard "single person" pricing, under the assumption that we're looking on behalf of a team of 5, 10, or more people.
</details>

<details>
<summary>
What does "Quote" mean in the Source column?
</summary>
If a vendor doesn't list pricing but a user has submitted pricing based on a quote, it can be included here. If a vendor feels that their actual pricing is inaccurately reflected by this quote, feel free to let me know and I'll update the page.
</details>

<details>
<summary>
I'm a vendor and this data is wrong!
</summary>
Please feel free to submit a PR to this page, or reach out at sso @ myGitHubUsername dotcom. I only want this data to be accurate.
</details>

<details>
<summary>
I'm a vendor and this doesn't reflect the value-add of our Enterprise tier!
</summary>
That's the point. Decouple your security features from your value-added services. They should be priced separately.
</details>

<details>
<summary>
But it costs money to provide SAML support, so we can't offer it for free!
</summary>
  While I'd like people to really consider it a <em>bare minimum</em> feature for business SaaS, I'm OK with it costing a little extra to cover maintenance costs. If your SSO support is a 10% price hike, you're not on this list. But these percentage increases are not maintenance costs, they're revenue generation because you know your customers have no good options.
</details>

## Footnotes
{% for vendor in vendors %}
{{ vendor.footnotes }}
{% endfor %}
{% for vendor in call_us %}
{{ vendor.footnotes }}
{% endfor %}

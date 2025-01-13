# Cloudflare Bypass

A tool to bypass Cloudflare protection and obtain cf_clearance cookies.

## Requirements
```
pip install -r requirements.txt
```
```
pip install javascript
```

# Example
```python
from aqua import CF_Solver


cf = CF_Solver('https://discord.com')
cookie = cf.cookie()
print(cookie)


# other
cf = CF_Solver('https://tempail.com')
cookie2 = cf.cookie()
print(cookie2)


# follow up requests
response = cf.client.get(url=url, timeout=10)
response = cf.client.post(url=url, data=data, json=json, timeout=10)

```

# Turnstile Reverse Engineering Progress
- Reversed challenge token:
![dev](https://github.com/LOBYXLYX/Cloudflare-Bypass/blob/main/images/20241107_171954.jpg)
![cons](https://github.com/LOBYXLYX/Cloudflare-Bypass/blob/main/images/20241107_172047.jpg)

- Challenge Request Reversed:
![ch](https://github.com/LOBYXLYX/Cloudflare-Bypass/blob/main/images/20241126_205308.jpg)

- small showcase

https://github.com/user-attachments/assets/407ee7d3-86e3-4d19-b3d9-8bd18c908ecc


discord: lyxz2


bash
pip install -r requirements.txt
pip install javascript


## Basic Usage

```python
from aqua import CF_Solver
```
Simple usage - just pass your target URL
```python
cf = CF_Solver('https://your-target-website.com')
cookie = cf.cookie()
print(cookie)
```

Making subsequent requests using the solver's client
```python
response = cf.client.get('https://your-target-website.com/some-path')
print(response.text)
```

For sites with Turnstile protection
```python
cf = CF_Solver(
'https://your-target-website.com',
siteKey='your-site-key-here' # Required for Turnstile
)
cf.solve_turnstile()
```

With custom headers
```python
cf = CF_Solver(
'https://your-target-website.com',
headers={
'authorization': 'your-auth-token',
'x-custom-header': 'custom-value'
}
)
```

## Advanced Options
- `userAgent`: Customize the User-Agent string
- `proxy`: Add proxy support
- `headers`: Add custom headers
- `clientRequest`: Use your own HTTP client instance


Example of my use case for v2ph.com

```python
from aqua import CF_Solver

# Common browser-like headers to appear more human-like
headers = {
    'accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8',
    'accept-language': 'en-US,en;q=0.9',
    'cache-control': 'max-age=0',
    'sec-ch-ua': '"Not A(Brand";v="99", "Google Chrome";v="121", "Chromium";v="121"',
    'sec-ch-ua-mobile': '?0',
    'sec-ch-ua-platform': '"Windows"',
    'sec-fetch-dest': 'document',
    'sec-fetch-mode': 'navigate',
    'sec-fetch-site': 'none',
    'sec-fetch-user': '?1',
    'upgrade-insecure-requests': '1'
}

# Create CF_Solver instance for v2ph.com
cf = CF_Solver(
    'https://www.v2ph.com',
    headers=headers,
    # You'll need to find the correct siteKey for v2ph.com
    # You can usually find this by inspecting the page source
    # or network requests when the Turnstile challenge appears
    siteKey='YOUR_SITE_KEY_HERE',
    # Using a common browser User-Agent
    userAgent='Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36'
)

# Solve the Turnstile challenge
cf.solve_turnstile()

# Make subsequent requests using the solver's client
response = cf.client.get('https://www.v2ph.com')
print(response.text)
```


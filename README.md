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

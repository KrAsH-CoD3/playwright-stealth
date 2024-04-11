# Playwright-Stealth

Helper scripts for avoiding bot detection of [playwright-python] controlled browsers.

Usage:
```
from playwright_stealth import stealth_async, StealthConfig

async with async_playwright() as pw:
    browser = await pw.chromium.launch(headless=True)
    context = await browser.new_context(**p.devices["Pixel 7"])
    page = await context.newPage()
    # Setting our desired value for the navigator property
    stealth_config = StealthConfig(
        navigator_plugins=False,
        navigator_hardware_concurrency= 8,
        nav_platform= 'Linux armv81',
        webgl_vendor= 'Google Inc. (Qualcomm)',
        webgl_renderer= 'ANGLE (Qualcomm, Adreno (TM) 640, OpenGL ES 3.2)',
    )
    await stealth_async(page, stealth_config)
    await page.goto('https://bot.sannysoft.com/')
    await page.screenshot(path='chrome_headless_stealth.png', fullPage=True)
```
## StealthConfig Arguments
Pass in your desired value
 - `vendor: str` = 'Intel Inc.'
 - `renderer: str` = 'Intel Iris OpenGL Engine'
 - `nav_platform: str` = None
 - `nav_user_agent: str` = None
 - `nav_vendor: str` = 'Google Inc.'
 - `languages: Tuple[str]` = ('en-US', 'en')
 - `navigator_hardware_concurrency: int` = 4
 - `runOnInsecureOrigins: Optional[bool]` = None

For more see `/bin/test_chrome.py` and `/bin/test_firefox.py`
and original puppeteer repo: https://github.com/berstend/puppeteer-extra/tree/master/packages/puppeteer-extra-plugin-stealth

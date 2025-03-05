# Bypass

### Captcha

- cloudflare with DrissionPage
```
driver = self.create_new_driver()
driver.get(target)
print(f"[{self.thread_id}] Browser started [PID: {driver.process_id}]")
time.sleep(8.0 if not self.summary.emulation_force else 12.0)

if "access denied" in driver.title.lower():
    raise Exception('Access Denied')

if "needs to review the security" in driver.html or "just a moment" in driver.title.lower():
    print(f'[{self.thread_id}] Captcha detected!')
    bypass_failed_times = 0
    while bypass_failed_times < 2:
        try:
            challenge_frame = driver.ele("ANTI COPY-PASTE", timeout=1).sr.ele("t:iframe", timeout=1) # Can be outdated in the future
            challenge_iframe_body = challenge_frame.ele("ANTI COPY-PASTE", timeout=1).sr
            challenge_button = challenge_iframe_body.ele("t:input", timeout=1)
            challenge_button.click()
            break
        except Exception:
            bypass_failed_times += 1
            print(f"[{self.thread_id}] {bypass_failed_times=}/2")
            time.sleep(2.0)

... LOGIC GOES HERE
```
https://github.com/g1879/DrissionPage/issues/329#issuecomment-2272276754

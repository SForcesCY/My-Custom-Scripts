# Fully Obfuscated Throttled API Requests with Auto Refresh and Button Click
Overview
This Tampermonkey script performs throttled API polling and automatic button clicks on a webpage. It is designed to fetch updates from two different API endpoints at specific intervals and handle interactions with the webpage by automatically clicking certain buttons or elements. The script uses obfuscation techniques to make it harder to reverse-engineer, ensuring that its functionality is hidden from casual inspection.

Key Features:
Polls a main API every second, queues updates, and displays them with a 5-second delay to avoid missing any updates.
Polls a scoreboard API every 3 seconds.
Automatically clicks a button or a specific table header (<th>) element on the webpage to interact with the DOM.
Refreshes the webpage automatically every 4 hours.
Uses advanced obfuscation techniques to protect sensitive logic, such as URL encoding, string splitting, and dynamic function reassembly.
How It Works
1. Throttled API Polling
The script polls the main API every second but ensures that no more than one request is made every 3 seconds (throttling). It compares the response from the API with the last stored response and only enqueues new data if a change is detected.

javascript
Copy code
function _nestedB() {
    return function() {
        const _0xC = Date.now();
        if (_0xC - _0x9 < _0xA) return;
        _0x9 = _0xC;

        fetch(apiUrl, {
            method: 'GET',
            headers: {
                'Cache-Control': 'no-cache'
            }
        })
        .then(_0xD => _0xD.json())
        .then(_0xE => {
            if (JSON.stringify(_0xE) !== JSON.stringify(_0x6)) {
                _0x7.push(_0xE);
                _0x6 = _0xE;
                if (!_0x8) {
                    _nestedF()();
                }
            }
        })
        .catch(_0xG => {});
    };
}
2. Queueing and Displaying Updates
The script maintains a queue of updates from the main API. It processes these updates one by one, displaying them every 5 seconds. This prevents missing updates that occur between polling intervals.

javascript
Copy code
function _nestedF() {
    return function() {
        if (_0x7.length === 0) {
            _0x8 = false;
            return;
        }
        _0x8 = true;
        _0x7.shift();
        setTimeout(_nestedF(), 5000);
    };
}
3. Automatic Button and Element Clicks
The script automatically clicks an HTML button or <th> element on the webpage. It waits for the page to load and then searches for the target element. If found, the element is clicked automatically.

javascript
Copy code
function _clickThElement() {
    const _0xJ = Array.from(document.querySelectorAll('th[role="columnheader"][style*="position: sticky; top: 0px; cursor: pointer;"]'));
    if (_0xJ.length > 0) {
        const _0xK = _0xJ.find(_0xL => {
            const _0xM = _0xL.querySelector('span');
            if (_0xM) {
                const _0xN = _0xM.innerHTML.replace('<br>', ' ').replace(/\s+/g, ' ').trim();
                return _0xN.includes('FTDs Day');
            }
            return false;
        });

        if (_0xK) {
            _0xK.click();
        }
    }
}
4. Auto-Refreshing the Page
Every 4 hours, the script automatically refreshes the webpage to ensure data is up to date.

javascript
Copy code
setTimeout(() => {
    window.location.reload();
}, _0x3);
5. Obfuscation Techniques
To enhance the security of the script, several obfuscation techniques have been applied:

String Splitting and Reassembly: Sensitive strings like URLs are split into smaller parts and reassembled at runtime. This makes it harder for someone to understand the URLs by simply inspecting the code.
javascript
Copy code
const _0x1 = _concatParts(['%68%74%74%70', '%73%3A%2F%2F%65', '%78%61%6D%70%6C%65%2E%63%6F%6D']);
const apiUrl = unescape(_0x1);
Nested Functions: Functions are nested within other functions, making the logic flow harder to track.
javascript
Copy code
function _nestedB() { /* code */ }
function _nestedF() { /* code */ }
Dynamic Element Searching: The script searches for and interacts with DOM elements dynamically, making it less obvious how it operates on the page.
How to Use This Script:
Install Tampermonkey in your browser.
Create a new script and copy the code into the Tampermonkey editor.
Update the apiUrl and scoreboardApiUrl with your own API endpoints (they must be URL encoded).
Save and enable the script.
Obfuscation Explanation
This script uses several obfuscation strategies to protect its functionality:

Percent-Encoding: URLs are obfuscated using percent-encoding (unescape() is used to decode them at runtime).
String Splitting: Strings are split into multiple parts and reassembled at runtime, which hides the meaning of key strings.
Variable Name Obfuscation: Most variable and function names have been obfuscated to nonsensical names to make the script harder to understand.
Minimal Logging: All console.log statements have been removed, except for the initial log that shows the script has been injected and is running.
Example of Encoded URL:
javascript
Copy code
const apiUrl = unescape('%68%74%74%70%73%3A%2F%2F%61%70%69%2E%6D%79%64%6F%6D%61%69%6E%2E%63%6F%6D%2F%65%6E%64%70%6F%69%6E%74');
Disclaimer
This script is designed for educational purposes and personal use. Be cautious when using obfuscated scripts, as they can be difficult to debug and maintain. Always thoroughly test scripts before deploying them in production environments.

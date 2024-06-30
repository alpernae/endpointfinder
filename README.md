# Endpoint Finder Bookmarklet

This bookmarklet scans the current webpage for endpoints and displays them in an overlay. The overlay provides a "Close" button to remove it from the view.

## Features

- Extracts endpoints from the current webpage and scripts.
- Displays the endpoints in a user-friendly overlay.
- "Close" button to remove the overlay.
- Endpoints are labeled with a likely HTTP method (e.g., `(likely GET)`).

## How to Use

1. Create a new bookmark in your browser.
2. Edit the bookmark and replace the URL with the following code:

    ```javascript
    javascript:(function(){var scripts=document.getElementsByTagName("script"),regex=/(?<=(\"|\'|\`))\/[a-zA-Z0-9_?&=\/\-\#\.]*(?=(\"|\'|\`))/g,results=new Set;function fetchAndExtract(e){""!==e&&fetch(e).then(function(e){return e.text()}).then(function(e){for(var t=e.matchAll(regex),r=0;r<t.length;r++)results.add({endpoint:t[r][0],method:"(likely GET)"})}).catch(function(e){console.error("An error occurred:",e)})}for(var i=0;i<scripts.length;i++)fetchAndExtract(scripts[i].src);var pageContent=document.documentElement.outerHTML,matches=pageContent.matchAll(regex);for(const match of matches)results.add({endpoint:match[0],method:"(likely GET)"});function displayResults(){var e=document.createElement("div");e.style.position="fixed",e.style.top="0",e.style.left="0",e.style.width="100%",e.style.height="100%",e.style.padding="20px",e.style.backgroundColor="rgba(0,0,0,0.8)",e.style.color="#fff",e.style.overflowY="auto",e.style.zIndex="9999";var t=document.createElement("div");t.style.maxWidth="800px",t.style.margin="0 auto",t.style.backgroundColor="#333",t.style.padding="20px",t.style.borderRadius="8px",t.style.textAlign="left";var closeBtn=document.createElement("button");closeBtn.textContent="Close",closeBtn.style.position="fixed",closeBtn.style.top="10px",closeBtn.style.right="10px",closeBtn.style.padding="10px",closeBtn.style.backgroundColor="#f44336",closeBtn.style.color="#fff",closeBtn.style.border="none",closeBtn.style.borderRadius="5px",closeBtn.style.cursor="pointer",closeBtn.addEventListener("click",function(){document.body.removeChild(e)}),e.appendChild(closeBtn),t.innerHTML+="<h2 style='color:#f1c40f;text-align:left'>Found Endpoints</h2>",0===results.size?t.innerHTML+="<p>No endpoints found.</p>":results.forEach(function(e){var n=document.createElement("div");n.innerHTML="<strong>"+e.endpoint+"</strong> - "+e.method,t.appendChild(n)}),e.appendChild(t),document.body.appendChild(e)}setTimeout(displayResults,3e3)})();
    ```

3. Save the bookmark.
4. Navigate to any webpage and click the bookmarklet to see the endpoints.

## Example

- Open a webpage.
- Click the "Endpoint Finder" bookmark.
- An overlay will appear, listing all the found endpoints.
- Click the "Close" button to remove the overlay.

## Screenshot

![Screenshot](https://github.com/alpernae/endpointfinder/blob/main/Screenshot.jpg)

## Notes

- The detected HTTP method is a best guess and may not always be accurate.
- Ensure your browser allows JavaScript execution from bookmarks.

## Contributing

Feel free to submit issues or pull requests if you find bugs or have improvements.

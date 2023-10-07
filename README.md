When testing a page build with elementor, you may find that the page can scroll right and left on mobile or tablet when it shouldn’t. This is usually caused by an element that is not positioned properly.

How to debug elementor to show you which element is causing the horizontal overflow
Visit the page in your browser
Open Developer Tools – Right Click, Inspect or Ctrl+Shift+I
You may already have this open to view the page on other device widths (Ctrl+Shift+M once Inspect is open)
Click on the Console tab
Paste the following code and then hit Enter
(function (d) {
    var w = d.documentElement.offsetWidth,
        t = d.createTreeWalker(d.body, NodeFilter.SHOW_ELEMENT),
        b;
    while (t.nextNode()) {
        b = t.currentNode.getBoundingClientRect();
        if (b.right > w || b.left < 0) {
            t.currentNode.style.setProperty('outline', '1px dotted red', 'important');
            console.log(t.currentNode);
        }
    };
}(document));

This will highlight the elements causing the overflow in a red box.
Scroll up and down the page to fine the elements highlighted in red.
Edit your page with elementor and adjust those elements to fix.

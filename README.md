1. Directly paste json file in n8n to use this workflow.
2. but setting up of credentials are required so after setting up ,the google bookmark connection is also needed to be established which needs pasting the test url(given by webhook node) in the required bookmark section.
3. For this you should know how to create a bookmark in google chrome which will do the webscraping .
4. right click on the bookmark bar and click add a page, rename the bookmark and paste this code in url section while putting your test url at the required section.
5. javascript:(function() {
    // 1. Ask for your thought process
    const userThoughts = prompt("Codeforces to PDF: Enter your approach, thoughts, or hints for this problem:");
    
    // If you click cancel, abort the script
    if (userThoughts === null) {
        return; 
    }

    // 2. Scrape the problem details from the Codeforces page
    const problemUrl = window.location.href;
    const problemTitle = document.title;
    
    // Grab the actual problem text (Codeforces uses the 'problem-statement' class)
    const problemElement = document.querySelector('.problem-statement');
    const problemText = problemElement ? problemElement.innerText : "Could not extract problem text.";

    // 3. Define your n8n Webhook URL
    // IMPORTANT: Replace this with your actual n8n Test or Production Webhook URL
    const webhookUrl = "YOUR_N8N_WEBHOOK_URL_HERE"; 

    // 4. Build the payload
    const payload = {
        url: problemUrl,
        title: problemTitle,
        problem_text: problemText,
        user_thoughts: userThoughts
    };

    // 5. Fire the POST request to n8n
    fetch(webhookUrl, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
        },
        body: JSON.stringify(payload)
    })
    .then(response => {
        if (response.ok) {
            alert("✅ Successfully sent to your n8n pipeline!");
        } else {
            alert("❌ Failed to send. Status: " + response.status);
        }
    })
    .catch(error => {
        console.error("Error:", error);

6. Then execute your workflow (more your refine the system prompt the better the output you will get)   
        alert("❌ Error sending data. Check browser console.");
    });
})();

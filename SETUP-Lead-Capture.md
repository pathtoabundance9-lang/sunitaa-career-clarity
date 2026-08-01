# Career Clarity Quotient — Setup Notes

## Deploy the page (2 minutes)
1. Go to **app.netlify.com/drop**
2. Drag this whole **Sunitaa-CCQ-Deploy** folder onto the page (both `index.html` and `sunitaa.jpg` must go up together).
3. Netlify gives you a live link instantly. Rename the site in Site settings if you like (e.g. `career-clarity-quotient.netlify.app`).
4. Share that link on WhatsApp / LinkedIn. To update later, just drag the folder on again.

The **booking button already works** — it opens Sunitaa's Cal.com 30-min link with the parent's name, email, score and gap pre-filled.

## Optional: also save every lead to a Google Sheet
The page books calls without this. Do it if you also want a running list of everyone who takes the quiz.

1. Create a Google Sheet (any name).
2. **Extensions → Apps Script**, delete the sample, paste:

```js
function doPost(e){
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var sheet = ss.getSheetByName('Leads') || ss.insertSheet('Leads');
  var d = JSON.parse(e.postData.contents);
  if(sheet.getLastRow() === 0){
    sheet.appendRow(['Date','Name','Email','WhatsApp','Score','Band / Class / Gap']);
  }
  sheet.appendRow([d.date || new Date(), d.name, d.email, d.whatsapp, d.score, d.band]);
  return ContentService.createTextOutput(JSON.stringify({ok:true}))
         .setMimeType(ContentService.MimeType.JSON);
}
```

3. **Deploy → New deployment → Web app**. Execute as **Me**, Who has access **Anyone**. Copy the web-app URL.
4. In `index.html`, replace `PASTE_YOUR_GOOGLE_APPS_SCRIPT_URL_HERE` with that URL.
5. Re-drag the folder to Netlify to update.

## Still to add later
- **The short video**: when Sunitaa's video is ready, embed it in `index.html` at the line marked `VIDEO SLOT`, just above the booking button.

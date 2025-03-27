# 📋 Konfront ESK (Encuesta de Satisfacción Konfront) Integration Guide

This `README.md` explains how to integrate the Konfront Satisfaction Survey (ESK) popup into your product using an iframe, conditional logic, and validation via API.

---

## 🚀 Step 1: Add the Popup

Add a popup to the pages where the ESK should be triggered.

> 💡 **Recommendation**: Create a reusable component for consistency and easier maintenance.

---

## 🧩 Step 2: Embed the ESK iframe

Insert the following code in the popup:

```html
<iframe 
  src="https://products.konfront.mx/encuesta_de_satisfaccion?name=[name]&email=[email]&UserUID=[UserUID]&color=[Color 1]&color2=[Color 2]&color3=[Color 3]&color4=[Color 4]" 
  style="height:280px;width:600px;" 
  title="ESK">
</iframe>
```

---

## 🧠 Step 3: Replace Parameters

Replace the placeholders in the iframe URL with actual values:

- `[name]`: Current user's name
- `[email]`: Current user's email
- `[UserUID]`: Unique ID of the user
- `[Color 1]`: Primary button color (e.g., `#FFFFFF`)
- `[Color 2]`: Secondary button color
- `[Color 3]`: Primary text color
- `[Color 4]`: Secondary text color

> ⚠️ All values must be URL encoded. Do **not** replace spaces with `+`.

---

## 📡 Step 4: Add Conditional Logic

Conditionally show the popup based on when it was last shown or answered. Use the following API to fetch this data:

### Endpoint
**POST** `https://products.konfront.mx/api/1.1/wf/esk_date_check`

### Headers
`Authorization: Bearer [API_KEY]`

### Body (form-data)
```
UserUID = [User's Unique ID]
```

### Example Responses

**No match:**
```json
{
  "status": "success",
  "response": {
    "ResultCount": 0
  }
}
```

**Opened but not answered:**
```json
{
  "status": "success",
  "response": {
    "ResultCount": 1,
    "UserUID": "1698182336701x843563954527648500",
    "Email": "test@konfront.mx",
    "Name": "Prueba Test Testing",
    "LastDateOpened": 1743098545087,
    "AnsweredBoolean": false
  }
}
```

**Answered:**
```json
{
  "status": "success",
  "response": {
    "ResultCount": 1,
    "UserUID": "1698182336701x843563954527648500",
    "Email": "test@konfront.mx",
    "Name": "test Prueba Testing",
    "LastDateOpened": 1743098545087,
    "AnsweredBoolean": true,
    "LastDateAnswered": 1743098640000
  }
}
```

---

## 🔐 Step 5: Request API Key

Ask **Ximena Vega** for the API key. Once added to your product, **delete it from all messages or emails** where it was shared.

---

## 🧪 Step 6: Run Tests

- Confirm popup displays under correct conditions
- Use Postman to verify data is saved correctly
- Confirm API returns correct values
- Confirm conditional logic properly handles each API response
- Validate behavior when no prior response exists

---

## ✅ Step 7: Final Steps

Notify **Ximena Vega** once the system is fully implemented and ready for final testing.

---

## 📞 Support
For API access or integration help, contact the Konfront Product Team.

// Function to set a cookie
function setCookie(name, value, days) {
  let expires = "";
  if (days) {
    const date = new Date();
    date.setTime(date.getTime() + days * 24 * 60 * 60 * 1000);
    expires = "; expires=" + date.toUTCString();
  }
  document.cookie = name + "=" + (value || "") + expires + "; path=/";
}

// Function to get a cookie
function getCookie(name) {
  const nameEQ = name + "=";
  const ca = document.cookie.split(";");
  for (let i = 0; i < ca.length; i++) {
    let c = ca[i];
    while (c.charAt(0) == " ") c = c.substring(1, c.length);
    if (c.indexOf(nameEQ) == 0) return c.substring(nameEQ.length, c.length);
  }
  return null;
}

// Function to check if session ID exists in URL parameters
function getSessionIdFromURL() {
  const urlParams = new URLSearchParams(window.location.search);
  return urlParams.get("session");
}

// Main function to handle session cookie
function handleSessionCookie() {
  const sessionId = getSessionIdFromURL();
  if (sessionId) {
    // Set the session ID as a cookie that expires in 7 days
    setCookie("sessionId", sessionId, 7);
    console.log("Session ID cookie set");
  } else {
    const existingSessionId = getCookie("sessionId");
    if (existingSessionId) {
      console.log("Existing session ID found:", existingSessionId);
    } else {
      console.log("No session ID found");
    }
  }
}

function indexCookie() {
  const existingSessionId = getCookie("sessionId");
  if (existingSessionId) {
    console.log("Existing session ID found:", existingSessionId);
    checkSession(existingSessionId)
  } else {
    console.log("No session ID found");
  }
}

function checkSession(sessionId) {
    var dataToSend = {
        sessionId: sessionId
    };

  // URL des Webhooks
  var webhookUrl = "https://hook.eu2.make.com/cvooe3c42pd0jmj5hwhwnrf86svsw1l6";

  // Sende die Variable an den Webhook
  $.ajax({
    url: webhookUrl,
    type: "POST",
    contentType: "application/json",
    data: JSON.stringify(dataToSend),
    success: function (response, textStatus, jqXHR) {
        console.log("Erfolgreich gesendet:", response);
        console.log("Statuscode:", jqXHR.status);
        if(jqXHR.status === 200 && response !== "Accepted") {
            $("#content").load("content/hello.html", function() {
                $("#response").html(response);
            });
          }
    },
    error: function (error) {
        console.error("Fehler beim Senden:", error);
        if (error.status === 401) {
            $("#content").load("content/auth.html");
        } else {
            $("#response").html(error);
        }
    },
  });


}

# iOS-Discord-OAuth2-bypass-

Discord only allows http(s) redirct uri for normal OAuth2 (not sure about PKC flow). But if your looking to get a iOS users Disocrd username and ID. You can use this very simple code, no need for a domain/backend to redirct the user. It basically pops open a sheet with a WKWebView and does a little trick to scrape the Local Storage and extract the username and uid. This method literally is taking me 0-1 seconds to get the dUID and dUsername, and no button clicks required.

you can put this view in a .sheet or any view. The isLoggedIn Binding bool could be used to show a loader while the Local Storage is being scraped after the user logs in. Most of the time the user does not need to login if they use discord on their phone.

# iOS-Discord-OAuth2-bypass-

Discord only allows http(s) redirct uri for normal OAuth2 (not sure about PKC flow). But if your looking to get a iOS users Disocrd username and ID. You can use this very simple code, no need for a domain/backend to redirct the user. It basically pops open a sheet with a WKWebView and does a little trick to scrape the Local Storage and extract the username and uid. This method literally is taking me 0-1 seconds to get the dUID and dUsername, and no button clicks required.

you can put this view in a .sheet or any view. The isLoggedIn Binding bool could be used to show a loader while the Local Storage is being scraped after the user logs in. Most of the time the user does not need to login if they use discord on their phone.

Example usage:

```
.sheet(isPresented: $showDiscordSheet, content: {
            DiscordWebView(username: $discordUsername, id: $discordUID, isLoggedIn: $isLoggedIn)
                .overlay(content: {
                    if isLoggedIn {
                        Color.gray.opacity(0.2).ignoresSafeArea()
                    }
                })
                .overlay {
                    if isLoggedIn {
                        VStack(spacing: 25){
                            Text("Authenticating...").font(.headline)
                            
                            LottieView(loopMode: .loop, name: "aiLoad")
                                .scaleEffect(0.7).frame(width: 100, height: 100)
                        }
                        .padding().background(.ultraThinMaterial)
                        .clipShape(RoundedRectangle(cornerRadius: 15))
                        .transition(.move(edge: .bottom).combined(with: .scale))
                    }
                }
                .overlay(alignment: .top, content: {
                    HStack {
                        Spacer()
                        Button {
                            UIImpactFeedbackGenerator(style: .light).impactOccurred()
                            showDiscordSheet = false
                        } label: {
                            Text("Cancel").font(.subheadline).bold()
                                .padding(.horizontal, 9).padding(.vertical, 5)
                                .background(Color.babyBlue).clipShape(Capsule())
                        }.buttonStyle(.plain).padding(.trailing).frame(height: 60)
                    }.ignoresSafeArea(edges: .top)
                })
        })
```

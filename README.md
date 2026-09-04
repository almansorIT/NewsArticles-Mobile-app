# NewsArticles

A mobile news reader built with **React Native + Expo**. Browse news by category,
open an article to read it in full, save the ones you like to a favorites list,
and write and manage your own articles right on the device.

Built as a mobile-apps lab project — it runs entirely on the client, with no
backend: the news feed is bundled sample data, favorites live in Redux, and
user-created articles are stored locally with AsyncStorage.

## What the app does

**Welcome screen** — an animated splash (expanding rings around the app logo)
that plays for ~2.5 seconds, then moves on to the home screen automatically.

**Home screen** — greets the user, shows a horizontally scrolling category strip
(Technology, Sports, Business, Entertainment, Health) plus shortcuts to *My News*
and *My Favorites*. Tapping a category filters the "Latest News" grid below it,
which lays the articles out in a two-column card grid with staggered image
heights. Tapping a card opens the article.

**Article detail** — the full article: large header image, title, category and
body text, with a back button and a ♥ / ♡ toggle that adds or removes the
article from favorites.

**Favorites** — every article you have hearted, in one list. Shows an empty
state when nothing is saved yet; tapping an entry reopens its detail screen.
Favorites are held in the Redux store, so they last for the current app session.

**My News** — your own articles. Lists everything you have written, with an
*Add* button, and edit and delete actions on each entry. The list refreshes
whenever the screen regains focus, so it always reflects the latest changes.

**News form** — the add/edit screen: title, image URL (with a live preview) and
a multi-line description. The same screen handles both creating a new article
and editing an existing one, then saves to AsyncStorage.

**Custom article view** — the read view for a user-created article, with its
image, title and content, plus the same favorite toggle.

## Tech stack

| Area | Choice |
| --- | --- |
| Framework | React Native 0.74 on Expo SDK 51 |
| Navigation | React Navigation (native stack) |
| State management | Redux Toolkit + React Redux |
| Local persistence | AsyncStorage |
| Animation | React Native Reanimated |
| Responsive layout | react-native-responsive-screen (`wp` / `hp`) |
| Builds | EAS Build |

## Project structure

```
App.js                    # Wraps the navigator in the Redux Provider
src/
  navigation/index.js     # Native stack: Welcome -> Home -> detail/form screens
  redux/
    store.js              # configureStore with the favorites reducer
    favoritesSlice.js     # toggleFavorite: add/remove an article by idArticle
  components/
    categories.js         # Horizontal category strip + My News / My Favorites
    articles.js           # Two-column article grid and card
  screens/
    WelcomeScreen.js      # Animated splash
    HomeScreen.js         # Categories + filtered article feed (sample data)
    ArticleDetailScreen.js# Full article + favorite toggle
    FavoriteScreen.js     # Saved articles
    MyArticlesScreen.js   # User-created articles (list, edit, delete)
    NewsFormScreen.js     # Create / edit a user article
    CustomNewsScreen.js   # Read a user-created article
```

## Getting started

```bash
npm install     # install dependencies
npm start       # start the Expo dev server
```

Then run it on a device or emulator:

```bash
npm run android   # Android emulator or device
npm run ios       # iOS simulator (macOS only)
npm run web       # in the browser
```

Or scan the QR code from `npm start` with the Expo Go app.

## Notes and limitations

- The news feed is hardcoded sample data in `HomeScreen.js` — there is no live
  news API behind it.
- Favorites are kept in Redux only, so they are cleared when the app restarts;
  user-created articles do persist, via AsyncStorage.
- Article images are referenced by URL, so a network connection is needed for
  them to load.

## License

MIT — see [LICENSE](LICENSE).

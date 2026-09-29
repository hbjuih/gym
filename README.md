# Gym Log

A personal gym tracker that installs on your phone like an app. Each gym is its own tab at the bottom, like sheets in Excel. Weights are in pounds.

## Files
- `index.html`: the whole app (HTML, CSS and JS in one file)
- `manifest.json`: app name, icon and colors for the home screen
- `sw.js`: service worker that makes it work offline at the gym
- `icon-192.png`, `icon-512.png`: home screen icons

## Put it on your phone (GitHub Pages, free)
1. Create a new public GitHub repo (for example `gym-log`) and upload all 5 files to it.
2. In the repo, go to **Settings → Pages**, set Source to **Deploy from a branch**, choose `main` / root, and save.
3. After a minute your site is live at `https://<your-username>.github.io/gym-log/`.
4. Open that link on your phone:
   - **iPhone:** in Safari, tap Share → **Add to Home Screen**
   - **Android:** in Chrome, tap ⋮ → **Add to Home screen** / **Install app**
5. Open it from the home screen icon. It runs full-screen and works without signal.

Netlify Drop (drag the folder onto app.netlify.com/drop) works too.

## Using it
- **Switch gyms:** tap the tabs at the bottom. Tap **+** to add a gym. Double-tap the current tab (or use ⋯) to rename it.
- **Add exercises:** add several at once, separated by commas.
- **Log a set:** open an exercise, set the weight and reps, tap **Add set**. The last numbers you used are filled in for you, and "Last time" shows what you did the previous session.
- **Bodyweight moves:** leave the weight at 0 and it shows as "BW".
- **History:** the History toggle shows every workout at that gym by date.

## Push / Pull / Legs days
The chips above your exercises are your workout days. Pick **Push** and add exercises, and they're saved to Push day. The app looks at your last workout (at either gym) and marks the next day in the rotation as **NEXT**, and it opens on that day. Each day shows how many of its exercises you've done today. Tap **+** to add a day like "Arms", or use **⋯ → Edit workout days** to rename or delete one. Move an exercise to another day from its own ⋯ menu.

## Effort rating
Before tapping **Add set**, tap how hard it was: **Easy**, **Solid** (the default), **Max**, or **Pain**. It resets to Solid after each set.
- If you hit the top of your rep range but some sets were **Max**, it won't tell you to go up yet.
- If you flag **Pain**, the next session suggests going lighter, and the rest timer stops.

## Rest timer
It starts when you add a set (default 2:00). Tap **+30s** or **Skip**, or tap the time to change the length (also in ⋯ → Rest timer). It beeps and vibrates on Android when done. On iPhone there's no vibration, the silent switch mutes the beep, and it only alerts while the app is open, so keep an eye on the bar.

## Progress chart
Each exercise shows a line of your **estimated 1-rep max** from your best set each session. It rises whether you add weight or reps, so you can see real progress even while you're adding reps at the same weight. Tap a dot to see that day's best set.

## Consistency tracker
Open **⋯ → Consistency tracker** to see a GitHub-style grid of the last 12 months across both gyms. Darker squares mean more sets. Tap a square to see what you did that day. Tap "Days this week" to set your weekly goal; the week streak counts weeks in a row where you hit it.

## Recommendations (how it decides)
Each exercise shows a suggestion at the top, based on "double progression":
1. Pick a rep range (default 8–12, change it in the exercise's ⋯).
2. Stay at a weight and add reps until **every** working set hits the top of the range.
3. Then add the smallest weight jump (default 5 lb) and start again at the bottom of the range.

Safety rules so you don't progress too fast:
- It only changes one thing at a time: weight **or** reps, never both.
- It never suggests a jump over ~10% heavier; it suggests more reps instead.
- After a weight increase, it holds you there until your reps recover.
- After 2+ weeks off an exercise, it suggests starting about 10% lighter.
- If you're stuck at the same weight for 3 sessions, it suggests dropping ~10% and building back up.

"Working sets" are your heaviest sets that day, so lighter warm-up sets don't throw it off. These are guidelines, not medical advice. Sharp pain means stop.

## Your data
Everything is saved on your phone only, with no account and no server. Use **⋯ → Back up all data** now and then to save a backup file, and **Restore from backup** to load it on a new phone.

Note: the home screen app and the Safari tab keep separate data on iPhone, so always log from the home screen icon.

## Making changes
Edit `index.html`, re-upload it, and bump `CACHE = 'gymlog-v1'` in `sw.js` (to `v2` and so on) so your phone picks up the new version. You may need to close and reopen the app twice.

# xLights Sequence Catalogue (web app)

The whole app is one file, `index.html`. Open it in a browser, choose your xLights show folder, and it builds a searchable catalogue of every sequence with album art, artist, vendor and length, and flags any sequence missing its song.

Your files are read by the browser on your own computer and never uploaded. Fix with Claude sends Claude the details of the sequences it's working on (names, paths, tags, lengths) and the results of its searches, but not your audio or sequence files. Google Drive upload sends the catalogue and your settings (never your Anthropic API key), so you can pick everything back up on another device.

## The password

The page asks for a password before showing anything. This is just to keep people who aren't you from stumbling onto the live site and poking around — it's not real security (anyone who reads the page's source could bypass it), so don't rely on it to protect anything sensitive. Enter it once per browser/device and it's remembered after that, including on a downloaded catalogue you open elsewhere (that's a separate "device" as far as the browser's concerned, so it'll ask once there too). If you ever want to change it, just ask Claude Code to set a new one.

## Opening it

**Quickest:** double-click `index.html` to open it in Chrome or Edge. Everything works except Google Drive upload, because Google sign-in needs the page to have a web address.

**For Google Drive upload, give it a web address,** either of these:

- Host it for free. Drag the folder onto app.netlify.com/drop, or put `index.html` in a GitHub repository and turn on GitHub Pages. You get an address like `https://yourname.github.io/xlights-catalogue/` that works from any computer.
- Or run it on your own machine. In this folder run `python -m http.server 8080` and open `http://localhost:8080`.

Hosting it doesn't expose your sequences: the page only reads folders you pick in your own browser.

## Browsers

Chrome and Edge are best. They remember your folders, so Rescan works with one click.

Firefox and Safari work too, but ask you to pick the folder again each session. Their dialog says "Upload", but the files stay on your computer.

The app needs an internet connection the first time it reads song tags each session, to load one small open-source library (jsmediatags, for song tags and album art).

## Using it

1. Click **Choose show folder** and pick the folder that holds your sequences. For many people this is their actual xLights show folder; for others it's more of a library — every sequence ever bought or downloaded, kept somewhere separate from the show they actually run. Either is fine for cataloguing.
2. If your songs live somewhere else, click **Add a music folder**. You can add several.
3. If the folder you picked in step 1 is a library rather than your real show, set your **layout folder** in Settings too (see "Matching a sequence to your own layout" below) so the app knows where your actual props are.
4. Search, filter by vendor or song status, sort, and switch between covers and a list. Press `/` to jump to search. Click any sequence for its full details.

The catalogue is saved in the browser, so it's there next time you open the page. Rescans are fast because only changed files are reread.

**Download catalogue** saves a single HTML file with all the album art built in, plus `songs_to_check.csv` when anything needs attention. The downloaded file is the full app, so opening it on another computer shows the catalogue straight away and can scan too.

## Genres

Every sequence can have a genre, so you can browse and build a show by style. The starting list is made for holiday shows: Classic Christmas, Rock 'n' Roll & Oldies, Christmas Pop, Country, Rock & Metal, R&B & Soul, Jazz & Swing, Orchestral & Instrumental, Religious & Choral, A Cappella, Kids & Movies, Electronic & Dance, Hip-Hop, Latin, Novelty & Comedy, Halloween, Other Holidays and Show Elements (intros, countdowns, announcements). Edit, reorder or add to it in Settings; the order there is the order genres are listed and sorted in.

**Finding sequences by genre**: click the genre chips under the search bar. Click several to combine them (for example Classic Christmas and Rock 'n' Roll & Oldies), and click All genres to clear. The count on the right shows how many sequences match and their total running time, which is handy when planning a show. "Sort by genre" lists them in your genre order, and the list view has a Genre column.

**Assigning genres**:

- **Automatically from the song file**, when its genre tag is specific (for example "Country" or "Hard Rock"). Vague tags like "Holiday" or "Christmas" are ignored.
- **One sequence**: open it and pick from the Genre menu under the artist. "New genre…" adds one to your list.
- **Many at once**: click **Select**, click the sequences you want (or **Select all shown** after filtering or searching, for example for an artist), then choose from **Set genre** in the bar at the bottom. Click **Done** when finished.
- **With Claude**: tick **Assign genres** in Fix with Claude. Claude judges by the recording rather than the song, so *Jingle Bell Rock* by Bobby Helms is Rock 'n' Roll & Oldies, while Hall & Oates' version is Christmas Pop. Genre suggestions are light work, so many fit in each request and a large library doesn't cost much. Review them like any other suggestion.

Your choices always win over the song file's tag and are kept across rescans.

## Links to each sequence on the vendor's site

A sequence's details show a **Sequence page** link to where that sequence is sold, handy for re-downloading updates, checking which song version it was made for, or buying more from the same vendor. The link comes from, in order:

- **The sequence file**, when the vendor wrote the product page into the sequence's website or notes field and the address mentions the song.
- **Claude**: tick "Find each sequence's page on the vendor's website" in Fix with Claude. Claude searches the vendor's site for each sequence, matching the version by file name or artist when a vendor sells several. This needs web search turned on, and the app only accepts addresses that actually appeared in Claude's search results, so links can't be made up. Suggestions not on the vendor's own site are marked so you can check them.
- **You**: click **Add link** (or **Change**) and paste the address.

When there's no link yet, **Find on Sequence Scout** opens sequencescout.com already searching for that song, where you can compare every vendor that sells a sequence for it, open the right one and paste its address with Add link. Another button searches the vendor's own site. Sequences that already have a link get a **Compare on Sequence Scout** button. (Sequence Scout asks automated tools not to read its pages, so these are links for you to click; Claude doesn't read it.) Links are kept across rescans and are included in the catalogue's data file and the songs-to-check list.

## Models and groups

Every sequence's details list the **Models** and **Groups** it uses, read from the sequence itself. Past eight, the list shows "+N more" so a sequence with dozens of props doesn't take over the page; click it to see the rest. You can search for a model or prop by name in the main search box, and the **group chips** under the genre chips let you filter to everything that uses a particular group (click several to combine them, the same way genre chips work).

Click **See your models** under the summary for the full picture: every model and group, how many sequences use it, and their total running time. Click any one to jump straight to those sequences. If your show folder has `xlights_rgbeffects.xml` (it normally does, since it's the file that lists every prop in your show), this view also lists props **no sequence uses yet**, handy for spotting something you added but never got around to sequencing.

## Matching a sequence to your own layout

A sequence bought from a vendor was made for *their* layout, with their own names for props: a vendor's "Arch 1" might be your "Arch A", or they might have four arches where you only have two.

**This needs your real show, not your sequence library.** If the folder you chose in step 1 above is a library of every sequence you've ever bought — which for most people is bigger than, and separate from, the show they actually run each year — it won't contain your own props; it only has whatever each vendor shipped. Comparisons need to come from your *actual* xLights show folder: the one with your real `xlights_rgbeffects.xml`. If that's a different folder from the one you scan, set it as your **layout folder** in Settings. If you skip this, the app has no real layout to compare against and tells you so wherever it would otherwise show a comparison, with a button to set one right there.

Once your layout folder is set, any sequence whose models or groups don't already match yours by name shows a **Compare with your layout** panel. For each one, a dropdown offers your closest-matching prop, already picked if the app found a good one, with "Not in my layout" if it didn't. The guess comes from two places:

- **Shape, when it can.** Some vendors include a small `.xmodel` file with the sequence describing the exact prop it was made for (its type, pixel count and so on). When one's there, the app compares it against your own props' real dimensions (from your layout folder's `xlights_rgbeffects.xml`) rather than guessing from names, which is far more reliable, since what a vendor calls a prop and what you call it are unrelated.
- **Name, otherwise.** The same closest-match search used for songs.

Change any dropdown yourself at any time. **Fix with Claude** can also suggest mappings for the ones nothing local resolved confidently (tick "Map models to your layout"); like every Claude suggestion, you review it before it counts.

Once you've matched a vendor's props to yours, click **See your models**, then **Save mapping**. This writes `maphints/catalogue-mapping.xmaphint` into your layout folder (your show folder if you haven't set one), asking permission and confirming before replacing it if it's there already.

That file is xLights' own "map hints" format — a different thing from the `.xmap` file you might already save and reload by hand after manually mapping a sequence in xLights' **Import Effects** window (that one's a plain mapping saved from one particular import; this one's reusable across every sequence from a vendor). To use it, in that same window:

- Click **Auto Map**. It tries its usual name-matching passes first, then automatically reads every `.xmaphint` file sitting in your show's `maphints` folder and applies those too — no need to browse for the file at all.
- Or click **Load Mapping** and pick `maphints/catalogue-mapping.xmaphint` yourself (its file picker accepts `.xmaphint` alongside `.xmap`/`.xjmap`).

Either way, every mapping you've confirmed applies to that vendor's sequences from then on, including ones you buy later — you don't need to redo this per sequence. **Clear mapping** removes everything you've matched so far from the catalogue (it doesn't touch a file you've already saved).

## Exporting a playlist for Falcon Player (FPP)

If you run your show through a Falcon Player (FPP) controller rather than from xLights directly, **Export FPP playlist** in the toolbar turns a set of sequences into a playlist file you can import into FPP.

Filter and sort the catalogue the way you want the playlist ordered, then click Export FPP playlist. To export only some sequences, click **Select** first, pick them (or filter and click **Select all shown**), then export; with nothing selected, everything currently shown is exported.

A couple of things worth knowing:

- **FPP plays rendered `.fseq` files, not `.xsq` sequences.** The playlist assumes each sequence's `.fseq` is named the same as its sequence file, which is what xLights does by default when you render and upload to a controller. Render and upload your sequences (and their songs) to FPP before importing the playlist there.
- The export dialog tells you how many of the sequences you're exporting still need a song, and, if your show folder or layout folder had any `.fseq` files in them when you last scanned, how many don't have one yet.
- In FPP, open the playlist editor and import the downloaded file.

## Exporting a spreadsheet

**Export CSV** in the toolbar, next to Export FPP playlist, works the same way: filter the catalogue first (by vendor, by genre chips, by search, by anything), then click it to download a spreadsheet of exactly what's shown — one row per sequence, with its title, vendor, genre, where its sequence file lives, and where its matched song lives. As with the FPP export, click **Select** first and pick specific sequences if you want only some of what's filtered; with nothing selected, everything currently shown goes in.

## What gets scanned

Every folder inside the show folder and your music folders is searched, however deep. The **scan report** (the link under the summary) shows how many folders and files were searched, what was found, and anything skipped or unreadable.

- `.xsq` sequences, `.xsqz` packages, and older xLights sequences saved as `.xml` (recognised by their contents, so xLights' own settings files are ignored).
- **Inside `.zip` files**: vendor downloads you never unzipped are opened and their sequences and songs are catalogued. Only the parts needed are read, so large zips don't slow things down much. If you've already unzipped a sequence elsewhere, the zipped copy is left out so it isn't listed twice.
- **Skipped**: xLights backup folders, hidden folders and anything in your skip list. Both are settings.
- If a folder or zip can't be read (permissions, damage), it's listed in the report and the rest of the scan carries on.

## Fix with Claude

The scanner handles the easy cases with fixed rules. **Fix with Claude** hands the rest to Claude, which works as an agent: for each batch of problem sequences it decides what to look up, uses tools to search your files and the web, checks what it finds, and suggests fixes.

What it works on, and how:

- **Missing or uncertain songs**: searches every song file (including inside zips) by file name *and* by title/artist tags, reads the tags of likely candidates, and compares each song's length with the sequence length. Different versions of a song (radio edit, live, remix) have different lengths, so this is how it tells them apart. Sequences that are clearly intros, countdowns or loops can be suggested as not needing a song.
- **Vendors**: uses the author, email, website and folder name as clues and searches the web to find the vendor's proper business name. Where it can, it suggests a vendor *rule* (for example `*glowseq.com*`) so every sequence from that vendor is covered at once, including ones you buy later.
- **Missing artists and titles**: from song tags, file names or a web search.
- **Album art**: searches Apple Music and picks the release whose artist and title match.

Nothing changes until you review. Each suggestion shows how sure Claude is and why ("tags match; song 3:05 vs sequence 3:05"). Accept or reject one at a time, or accept everything Claude was at least 90% sure about. Accepted changes are kept across rescans, the "Changed by Claude" filter shows them, and **Undo Claude's changes** in a sequence's details reverses them. Claude can only suggest files it actually found and images it actually searched for; anything else is rejected.

**Setting it up**

1. Create an API key at console.anthropic.com (Settings, API keys) and add some credit. Usage is billed to that account.
2. Click **Fix with Claude**, paste the key, choose what to work on, and click **Start**.
3. For web search, an admin of your Anthropic account needs to turn web search on in the Claude Console. If it's off, Claude carries on without it and tells you.

The key is sent only to Anthropic. By default it's forgotten when you close the tab; tick "Remember the key on this device" to keep it in this browser. It's never included in downloaded catalogues or exported settings. Only use this on a computer you trust.

**Cost**: the activity panel shows the tokens used. Sonnet is a good balance; Haiku is cheaper for large libraries; Opus is the most thorough. Web search adds a per-search fee. Try a first run with just songs selected to get a feel for it.

## How songs are matched

- **Song found**: the song the sequence points to is in your show folder or a music folder, or packaged in the `.xsqz`. Sequences from vendors often point to the vendor's own `C:\Users\...` path; the app finds the song by file name, like xLights does.
- **Check song**: no exact match, but a file with a very similar name was found. Confirm it's the right track.
- **No song**: nothing found. These are listed in the red banner and in `songs_to_check.csv`.
- **No song needed**: you marked it, or it's an xLights Animation sequence with no media.

## Fixing missing songs

Click **Review them one by one** in the banner to step through every sequence that's missing its song or needs checking. You can also open any sequence from the grid and use Previous and Next. When you fix one, the next one opens automatically.

For each sequence you can:

- **Confirm a guessed song**: for "Check song" sequences, listen to the match and click **Yes, use it**. Its length is shown next to the sequence's length; a big difference usually means a different version of the song (radio edit, live, remix).
- **Pick a song from your folders**: the closest matches by file name, title and artist are listed, with their lengths. Listen to any of them, or search, then click **Use**.
- **Add a song file from your computer**: for example one you've just bought. In Chrome and Edge you can **save it into your show folder**: it's copied next to the sequence and named the way the sequence expects, so xLights finds it too. Other browsers can't save into folders, so the catalogue remembers the file and reminds you to copy it into your show folder yourself.
- **Continue without a song**: for intros, countdowns and other sequences that don't need one. For whole groups, add patterns in Settings, such as `Intros/*` or `*Countdown*`.
- **Find or buy the song**: the vendor's own song link when the sequence includes one, the vendor's website, a search of the vendor's site for the song, and searches on Amazon and Apple Music.

Choices are kept across rescans. **Undo changes to this sequence** reverses them.

## Vendor names

The app uses the author, email and website that vendors put in their sequences. To merge variations into one name, add lines in Settings like:

```
Acme Pixel Co = *acmepixel.com*, Acme*, Vendors/Acme/*
```

If you keep a folder per vendor, turn on "Use the top folder name as the vendor".

Settings can be exported and imported. The desktop version's `config.json` can be imported directly.

## Google Drive setup

This takes about five minutes, once. Google requires every app to have its own client ID.

1. Go to console.cloud.google.com and create a project, for example "xLights Catalogue".
2. In APIs & Services, open Library, find **Google Drive API** and click Enable.
3. In APIs & Services, open **OAuth consent screen**. Choose External, enter an app name and your email, and add yourself as a test user.
4. In **Credentials**, click Create credentials, then OAuth client ID. Choose **Web application**.
5. Under **Authorized JavaScript origins**, add the address you open the app from, with no path: for example `https://yourname.github.io` or `http://localhost:8080`.
6. Copy the client ID (it ends in `.apps.googleusercontent.com`) into the app's Settings.

Click **Upload to Google Drive** and sign in. The app uploads the catalogue, a data file, the songs-to-check list, and your settings (vendor names, genres, exempt patterns, model mappings and everything else in Settings, but never your Anthropic API key) to a Drive folder called "xLights Catalogue", replacing them on each upload so shared links keep working.

The app only asks for Google's most limited Drive permission: it can see and change files it created, and nothing else in your Drive.

Drive shows HTML files as downloads rather than web pages. To view the catalogue from Drive, download it and open it in a browser.

**Picking up on another device**: on a new computer or browser with nothing set up yet, add your Google Drive client ID in Settings (step 6 above — the same one, or a new one if the new address needs its own), then click **Load from Google Drive** on the opening screen. This brings down your catalogue and every setting, so your song matches, vendor rules, genres and model mappings are all there already. You'll still click **Choose show folder** yourself afterwards — browsers don't let a page remember *which* folder you picked on a different device, only on the one you picked it on.

## Troubleshooting

- **"Could not load cdn.jsdelivr.net"**: the page couldn't reach the internet to load its libraries. Check your connection and scan again.
- **Google says "origin not allowed" or "redirect_uri_mismatch"**: the address in step 5 must exactly match the one in your browser's address bar, including `http` or `https` and the port.
- **"No ... folder found in Google Drive"** when loading: either nothing's been uploaded from another device yet, or you used a custom Drive folder name there — set the same name in Settings before trying again.
- **A song you have shows as "No song"**: add the folder it's in with Add a music folder. If the file name is very different from what the sequence expects, rename the song or retarget the sequence in xLights.
- **"No real layout found yet" on the Models page or a sequence's details**: the folder you scan for sequences doesn't have your own `xlights_rgbeffects.xml` — normal if it's a library of vendor downloads rather than your actual show. Set your layout folder in Settings.
- **Start fresh with a rescan**: Settings, then Clear saved data. Forgets the saved catalogue, remembered folders and cached song details; your settings and accepted Claude changes are kept.
- **Start completely fresh**: Settings, then Reset everything. This forgets your settings too — vendor names, genres, exempt patterns, model mappings, every song and vendor you've fixed, and your Anthropic API key if you saved one. Export settings first if you want a copy; there's no undo.
- **"Your Anthropic API key was not accepted"**: check the key, and that the account has credit.
- **Claude says it's busy**: the app waits and retries automatically. Large libraries can hit your account's rate limit; smaller batches or Haiku help.

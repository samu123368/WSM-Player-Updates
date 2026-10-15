# Resources from your own Wii

Settings, setup, HOME and Message Board use live layouts, textures, HTML and
fonts from the installed System Menu on NAND. Scrollbar artwork is decoded in
memory from the installed EULA channel's Opera skin. No Wii UI screenshot packs,
extracted SD image folders or embedded Nintendo screenshot atlases are used.
The runtime does not export, cache or install these resources. Missing required
System Menu resources still use the existing resource-loading error path.

Installed channel banners/icons come from NAND. User-added WADs, homebrew icons,
personal photos and selected custom themes remain separate, supported features;
they are not copied Wii settings screenshot packs and are not deleted.
Frame captures used during HOME/menu animations stay in RAM, never image files.

## Japanese Forecast artwork

Japanese Forecast layout/artwork is read from the Japanese Forecast Channel
(HAFJ) on NAND. If that channel is absent, the installed regional channel's
artwork remains. There is no extracted local-assets fallback and WSM does not
download or install another region's channel.

## Historical agreement

The installed EULA channel supplies its original frame. Its full historical
online contract text is not stored in NAND. The frame reports that limitation;
acceptance of missing text is disabled. SD contract screenshots are not loaded.
If the EULA channel itself is absent, an explanatory page with Back is shown.
WSM never submits an agreement online.

## Original application resources

The WSM app icon and placeholder homebrew card are original generated artwork,
not copied Wii UI. Sample weather/news records and OFL Noto fallback glyphs are
also retained. Native HOME language labels are read from NAND, not an embedded
generated label-image pack. This change does not establish blanket clearance
for all code dependencies, text or trademarks, or authorize public publishing.

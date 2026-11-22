# Changelog

All notable changes to `qalainau/filament-warp-painter` are documented here.

## [Unreleased]

## [1.0.2] - 2026-11-22

### Fixed

- In a field with `multiple()`, editing a picture that was not first in the field sent the edited picture to the front and changed the order. The edited picture now takes the place of the original one, and the order is saved with the form.
- Choosing another tool (Arrow, Pen and so on, or its key) while cropping threw the frame away, so the picture kept its old size. It now crops to the frame first, as Apply and Done do. Cancel, Esc and Undo still leave the picture as it was.

## [1.0.1] - 2026-11-21

### Changed

- Crop: drag over the picture to draw the frame, the same way as Blur. Dragging inside the frame still moves it, and its corners and edges still resize it. With a shape such as 1:1 chosen, the drawn frame keeps that shape. The hint under the picture says so in all ten languages.

### Fixed

- Pressing Done while cropping threw the frame away and saved the picture at its old size. Done now crops to the frame first, as Apply does.
- On phones, Apply and Cancel of the crop bar were off the right edge of the screen. The crop bar now wraps onto two rows.

## [1.0.0] - 2026-11-20

### Added

- `->painter()` on `FileUpload` and `SpatieMediaLibraryFileUpload`: the pencil button of an uploaded picture opens a full-screen editor, and a **New picture** button under the field starts one from scratch. Done puts the picture back into the field, which uploads and saves it as usual.
- Tools: select (move, resize, rotate), pen, highlighter, line, arrow, rectangle, ellipse, text (plain, outlined, box, rounded label), numbers that count up, image (from the device, pasted, dropped, or from a list set with `images()`), blur and crop (free, fixed shapes, exact sizes, rotate). Undo and redo, zoom, keyboard shortcuts, mouse, pen and touch.
- Layers: every item can be hidden, locked, reordered, duplicated and deleted. Hidden items are left out of the saved picture.
- Pictures stay editable: the layers are kept on the server and found again through an ID written into the picture file (PNG, JPEG and WebP), whatever the file is renamed to and wherever it is stored. `reeditable(false)` keeps nothing.
- Blurred areas (mosaic, blur, solid box) are burned into the picture on Done: the original pixels are not kept in the file, the layers or the stored pictures, and the layers of earlier, unblurred edits of the same picture are deleted.
- Templates shared by everyone, per list (`templates('banners')`), with locked items and a permission for who may save and delete them (`canManageTemplates()`).
- Form values in text: `{title}` shows the value of the `title` field of the form (`fields()`), or a fixed value (`values()`).
- Settings per field: `tools()`, `colors()`, `sizes()`, `fonts()`, `images()`, `newPicture()`, `output()` and `maxSize()`.
- Settings per panel on `FilamentWarpPainterPlugin`: `disk()`, `directory()`, `maxAssetSize()`, `canManageTemplates()` and `tenantKeyUsing()`.
- `php artisan warp-painter:prune` removes layers nobody opened for a while and stored pictures nothing uses.
- Filament tenancy: layers and templates belong to the tenant they were made in. `php artisan warp:assign-tenant` gives existing rows to a tenant.
- Ten languages: English, Japanese, German, French, Spanish, Italian, Brazilian Portuguese, Korean, simplified and traditional Chinese.
- **Static analysis**: the methods added with `macro()` (`FileUpload::painter()`) are known to Larastan: the plugin ships `extension.neon`, a PHPStan extension that reads Filament's macros (loaded automatically with `phpstan/extension-installer`; otherwise add it to `includes`). See “Static analysis” in the README.
- **Static analysis**: the setting methods of the plugin class are declared as returning the plugin, so `$panel->plugin(…::make()->…())` passes Larastan.

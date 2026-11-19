GALAXY LOVE 2.0 - HEART GALAXY EDITION

FILES
- index.html
- styles.css
- script.js
- assets/photo-1.jpg ... assets/photo-8.jpg
- assets/central-couple.jpg (anh trung tam do ban vua gui)
- assets/love-song.mp3 (bai nhac ban da gui)

CHAY
1. Giai nen ZIP.
2. Mo index.html tren hosting hoac chay local server.
3. Neu mo bang may tinh: python -m http.server 8000, sau do vao http://localhost:8000
4. Neu dua len OneCompiler: HTML vao tab HTML, CSS vao tab CSS, JS vao tab JavaScript; upload thu muc assets va giu nguyen duong dan.

TUONG TAC
- Cham "CHAM VAO TINH CAU..." de vao galaxy va bat nhac.
- Vuot mot ngon de xoay khong gian 3D.
- Chum/tach hai ngon de zoom tren dien thoai; cuon chuot de zoom tren may tinh.
- Anh nam tren quy dao 3D nhung mat anh luon huong ve camera, khong bi meo theo goc xoay.
- Cham anh de xem anh lon.
- Cham tinh cau trung tam: hang nghin hat sang tu hoi thanh trai tim, dap nhip, bung thanh bui sao, sau do mo album ky niem.
- Nut nhac cho phep bat/tat nhac.

HIEN UNG TRAI TIM
Hieu ung trai tim duoc viet lai bang Canvas 2D va requestAnimationFrame, lay y tuong tu cac doan Particle Pool/Heart ma ban gui:
- Tao hinh trai tim tu cac diem tham so.
- Hat sang mau hong, tim, trang va xanh ngoc.
- Nhap nhip, phat sang, sau do tan ra thanh bui sao.
- Tu dong toi uu so hat theo kich thuoc man hinh va gioi han devicePixelRatio de tranh qua tai.

LUU Y
Trinh duyet co the chan tu dong phat nhac. Nhac se duoc thu phat sau thao tac cham vao trang dau; neu chua phat, cham nut ♫.


GALAXY 3D ENGINE UPDATE
----------------------
The 3D scene is rendered by galaxy3d.js using Three.js ES modules from jsDelivr.
An internet connection is required to load Three.js.

Interaction:
- Drag one finger / mouse to orbit the galaxy.
- Pinch two fingers / mouse wheel to zoom; zoom range is expanded for inspecting tiny photo-stars.
- Use the + / - buttons for zoom, 360° to pause/resume automatic rotation, and ↺ to reset the camera.
- Your uploaded couple portrait is placed at the center of the galaxy and can be tapped to view full size.
- Tap a floating photograph to open it.
- Tap the central planet to launch the particle-heart gift.
- The galaxy rotates gently when idle.

The 3D distribution is inspired by the radial/spiral distribution approach in
the Galaxy Visualization source supplied by the user (Michael Pascale, 2019).
Retain the BSD 2-Clause notice when redistributing that source or derivative
portions. Three.js is separately licensed under MIT.


IMAGE DISPLAY FIX + TOUCH-ONLY CONTROLS
---------------------------------------
- Added photo-assets.js, which embeds all eight memory photos and the central couple portrait as data URLs. This prevents empty/black photo frames when the editor or hosting does not publish the assets/ folder.
- index.html loads photo-assets.js before script.js and galaxy3d.js.
- Removed the on-screen zoom/rotation buttons. Rotate by dragging/swiping on the galaxy; zoom with a two-finger pinch on touchscreens or mouse wheel on desktop.
- Keep photo-assets.js, script.js, galaxy3d.js, styles.css, and index.html together if uploading files individually.
- The background music still uses assets/love-song.mp3, so keep the assets folder for music playback.


PATCH: CENTRAL PHOTO DISPLAY + PERFORMANCE
==========================================
This patch is based on the "Galaxy Love 2.0 - Touch & Photo Fix" package.

Central photo fix:
- Removed the large flat couple-photo billboard that sat in front of the center and hid the planet.
- Integrated the supplied couple portrait into the planet's spherical photo mosaic.
- The central globe now uses a compact 6 x 3 photo layout with the couple portrait in the middle area.
- Kept the central sphere clickable so it still opens the memory album.

Performance work:
- Reduced galaxy stars from 6,500/10,500 to 1,500/3,200 (mobile/desktop).
- Reduced distant stars, dust, orbit motes and photo-stars.
- Reused one glow texture/material for all photo-stars instead of creating a separate 256px canvas texture for every star.
- Reduced sphere/ring geometry detail and capped device pixel ratio.
- Limited rendering to about 30 FPS on mobile and 40 FPS on desktop.
- Added a WebGL capability probe and a lightweight Canvas fallback.
- Compressed the supplied JPEG photos and rebuilt photo-assets.js with the optimized image data. The audio file is unchanged.

OneCompiler:
1. Keep index.html, styles.css, script.js, galaxy3d.js and photo-assets.js together.
2. Keep the assets folder, including love-song.mp3 and all JPEG files.
3. Keep photo-assets.js before script.js and before galaxy3d.js (as in the supplied index.html).
4. Do not remove the Three.js CDN script line from index.html.

- Music preload is deferred until the user starts playback, reducing initial page loading.


PATCH: NATURAL PHOTO COLORS ON THE CENTER GLOBE
==============================================
- Changed the central photo-globe from a purple-emissive lit material to an unlit photo material, so scene lights no longer tint the pictures.
- Removed the purple translucent wash painted over every photo tile.
- Kept the purple atmosphere/corona outside the sphere for the galaxy mood, without applying it over the photo pixels.
- Reduced the dark purple vignette in the Canvas fallback.


PHOTO UPDATE: NEW MEMORIES ON THE OUTER ORBIT
============================================
- The central globe now uses only photo-1.jpg through photo-8.jpg plus
  central-couple.jpg. This keeps the center visually focused and avoids
  mixing the newly added photos into the central sphere.
- photo-9.jpg through photo-13.jpg are displayed as separate framed photos
  on the OUTER orbit around the central globe.
- All 13 photos can be opened by tapping/clicking them, and all 13 appear
  in the memory album.
- The five newer photos remain embedded in photo-assets.js for OneCompiler.
- The outer photo cards orbit independently and remain billboard-facing,
  so the pictures stay upright while the galaxy rotates.


IMAGE SHARPNESS UPDATE
- Central photo globe atlas increased from 1024x512 to 2048x1024.
- Photo textures use sRGB color, mipmaps, linear filtering, and up to 8x anisotropic filtering (device-supported maximum).
- Rendering pixel ratio raised moderately for clearer photos while retaining a mobile/desktop cap to control GPU load.
- Canvas fallback uses high-quality image smoothing.
- Original photo files are kept unchanged. Sharpness is still limited by the resolution of each source photo; upscaling cannot recreate detail that is not present in the original.

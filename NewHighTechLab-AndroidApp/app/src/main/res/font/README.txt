HOW TO USE THE REAL "NATIVINE" FONT
====================================

Right now the "Built by Kn Soft" splash text uses Android's built-in
"cursive" font family, so the app builds and looks handwritten-style
immediately with zero setup.

To use the actual Nativine font instead:

1. Get a licensed copy of the font file and rename it to: nativine.ttf
   (Font file names in Android must be lowercase, no spaces.)

2. Place it in this folder:
   app/src/main/res/font/nativine.ttf

3. Open:
   app/src/main/res/layout/activity_splash.xml

4. Find this line on the splashTagline TextView:
   android:fontFamily="cursive"

   and change it to:
   android:fontFamily="@font/nativine"

5. Rebuild the app. That's it.

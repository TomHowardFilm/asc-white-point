-- ASC White Point / CCT+Tint controller for grandMA3 (v1.5)

-- Created by:
-- Tom Howard
-- Spectre Lighting, Inc.
-- Last updated: March 2026

-- The purpose of this script is to allow you to run your fixtures in their native CIE xy profiles
-- and give you the tools to adjust CCT and Tint along the Planckian locus.
-- References ASC White Point LUT data, published by Tim Kang,
-- and expanded to include CCTs for every 100K, and Tint values for every 1/8th.

-- Do not run this plug-in directly within MA3.
-- Instead, you will use separate Macros in MA3 that will call specific functions in this script.
-- The functions in this script will read the current CIE_X and CIE_Y values of your selected Fixture(s)
-- It will then locate the nearest coordinate on the LUT table, and then adjust your fixture in the desired direction
-- Note: If your Fixture Profile types use another attribute other than "CIE_X" and "CIE_Y", the script needs to be adjusted.

-- ============================================================
--                           MACROS 
--             Create these in your MA3 Showfile
--              Or import them from this package
--       (Feel free to change the labels of the Macros,
--      as long as the macro script line remains the same)
-- ============================================================

-- Macro 1: "+100K CCT"
--   Line 1: Call Plugin "ASC White Point" "CCT_UP"

-- Macro 2: "-100K CCT"
--   Line 1: Call Plugin "ASC White Point" "CCT_DN"

-- Macro 3: "+1/8 Tint (greener)"
--   Line 1: Call Plugin "ASC White Point" "TINT_UP"

-- Macro 4: "-1/8 Tint (magenta)"
--   Line 1: Call Plugin "ASC White Point" "TINT_DN"

-- Macro 5: "Neutral Tint"
--   Line 1: Call Plugin "ASC White Point" "NO_TINT"

-- Macro 6: "What's my CCT"
--   Line 1: Call Plugin "ASC White Point" "REPORT"

-- Macro 7: "Input CCT"
--   Line 1: Call Plugin "ASC White Point" "INPUT"

-- ============================================================

-- NOTES:
-- 1) For Kino Flo xy fixtures to work (or any other fixture with a CIE xy range of 0.000-0.850),
--      enter your Patch and add the Tag "CIE_Extended" to these fixtures. The plugin will
--      now work correctly for these fixtures.
-- 2) Make sure your Encoder Bar readout is set to either Natural or Physical, basically anything
--      that shows you xy values in the correct 0.00-0.80 range. If, for example, the readout is
--      in Percent, the plugin will still attempt to enter coordinates in a low decimal value
--      and your lights will most likely snap to a full blue color.
--      Simply change the Encoder readout to correct this.
-- 3) If your existing xy values are a saturated party color, using one of the macros will snap you
--      back to the nearest LUT coordinate, which will be far away from your starting xy values.
--      In other words, this toolset is meant for adjusting white color only.
--      Similarly, if you use the "What's my CCT" Macro and you're in a saturated color,
--      the information displayed will be inaccurate.

---
title: Introduce new ColorScheme roles for Material 3
description: >-
  'ColorScheme' introduces new color roles to
  better align with Material Design 3.
  The 'ColorScheme.fromSeed' method is also updated to
  support the newly added colors.
---

## Summary

New color roles in `ColorScheme` include seven tone-based surfaces and
containers, and twelve accent colors for primary, secondary, and tertiary groups.
This update deprecates three existing color roles: `background`, `onBackground`,
and `surfaceVariant`. The `ColorScheme` constructed by the updated 
`ColorScheme.fromSeed` method now generates different values compared to the 
previous version, adapting to Material Design 3's guidelines.

## Background

The tone-based surface colors include: `surfaceBright`, `surfaceDim`,
`surfaceContainer`, `surfaceContainerLow`, `surfaceContainerLowest`,
`surfaceContainerHigh`, and `surfaceContainerHighest`. These changes help 
eliminate the use of widgets' `surfaceTintColor`, and replace the old 
opacity-based model which applied a tinted overlay on top of surfaces based 
on their elevation.  

The default `surfaceTintColor` for all widgets is now null and their default
background color is now based on the new tone-based surface colors.

`ColorScheme.fromSeed` has also been updated to use the latest algorithm from
the Material color utilities package. This change prevents the constructed 
`ColorScheme` from being too bright, even if the source color looks bright and
had a high chroma (contained little black, white, and shades of grey).

## Migration guide

The differences caused by the updated `ColorScheme.fromSeed` and the new color
roles should be small and acceptable. However, when providing a brighter
seed color to `ColorScheme.fromSeed`, it might construct a relatively darker
version of `ColorScheme`. To force the output to still be bright, set 
`schemeVariant: FromSeedVariant.fidelity` in `ColorScheme.fromSeed`. For 
example:

Code before migration:

```dart
ColorScheme.fromSeed(
    seedColor: Color(0xFF0000FF), // Bright blue
)
```

Code after migration:

```dart
ColorScheme.fromSeed(
    seedColor: Color(0xFF0000FF), // Bright blue
    schemeVariant: FromSeedVariant.fidelity,
)
```

The Material Design 3 removes 3 colors. To configure the appearance of the
material components, the `background` should be replaced with `surface`;
`onBackground` should be replaced with `onSurface`; `surfaceVariant` should be
migrated to `surfaceContainerHighest`.

Code before migration:

```dart
final ColorScheme colorScheme = ColorScheme();
MaterialApp(
  theme: ThemeData(
    //...
    colorScheme: colorScheme.copyWith(
      background: myColor1,
      onBackground: myColor2,
      surfaceVariant: myColor3,
    ),
  ),
  //...
)
```

Code after migration:

```dart
final ColorScheme colorScheme = ColorScheme();
MaterialApp(
  theme: ThemeData(
    //...
    colorScheme: colorScheme.copyWith(
      surface: myColor1,
      onSurface: myColor2,
      surfaceContainerHighest: myColor3,
    ),
  ),
  //...
)
```

Custom components that used to look up `ColorScheme.background`,
`ColorScheme.onBackground`, and `ColorScheme.surfaceVariant` can look up the
`ColorScheme.surface`, `ColorScheme.onSurface` and
`ColorScheme.surfaceContainerHighest` instead.

Code before migration:

```dart
Color myColor1 = Theme.of(context).colorScheme.background;
Color myColor2 = Theme.of(context).colorScheme.onBackground;
Color myColor3 = Theme.of(context).colorScheme.surfaceVariant;
```

Code after migration:

```dart
Color myColor1 = Theme.of(context).colorScheme.surface;
Color myColor2 = Theme.of(context).colorScheme.onSurface;
Color myColor3 = Theme.of(context).colorScheme.surfaceContainerHighest;
```

## Timeline

Landed in version: 3.21.0-4.0.pre<br>
In stable release: not yet

## References

Relevant issues:

* [Support tone-based surface and surface container ColorScheme roles][]
* [Support fidelity variant for ColorScheme.fromSeed][]

Relevant PRs:

* [Introduce tone-based surfaces and accent color add-ons - Part 1][]
* [Introduce tone-based surfaces and accent color add-ons - Part 2][]
* [Enhance ColorScheme.fromSeed with a new variant parameter][]

[Support tone-based surface and surface container ColorScheme roles]: {{site.repo.flutter}}/issues/115912
[Support fidelity variant for ColorScheme.fromSeed]: {{site.repo.flutter}}/issues/[144649]
[Introduce tone-based surfaces and accent color add-ons - Part 1]: {{site.repo.flutter}}/pull/[142654]
[Introduce tone-based surfaces and accent color add-ons - Part 2]: {{site.repo.flutter}}/pull/[144273]
[Enhance ColorScheme.fromSeed with a new variant parameter]: {{site.repo.flutter}}/pull/[144805]

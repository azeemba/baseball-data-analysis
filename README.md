Baseball data analysis
======================


Based on: https://www.kaggle.com/pschale/mlb-pitch-data-20152018/data

Using the analysis for the baseball video game.


# Conclusions copied from analysis.ipynb


# Starting location by handedness

Starting x:

```
{'ALL_R': [-2.1500, -1.6900, -1.2600], 'ALL_L': [1.4000, 1.9100, 2.3800]}
```

Starting y: 

```
50ft
```

Starting z:

```
 {'ALL_R': [5.5000, 5.7800, 6.0600], 'ALL_L': [5.5400, 5.8100, 6.1000]}
```

# vy0 by pitch type (feet per second)

```
{'FF': [-138.3300, -135.8800, -133.4300],
 'SL': [-126.3600, -123.3600, -120.1300],
 'CH': [-126.2900, -123.3100, -119.9200],
 'FT': [-137.3000, -134.9200, -132.3000],
 'SI': [-136.7400, -134.1100, -131.0800],
 'KC': [-119.9275, -117.5400, -115.0825],
 'CU': [-117.9200, -114.6300, -110.8200],
 'FC': [-131.4300, -128.4100, -125.9300],
 'FS': [-126.2700, -124.0100, -121.5600]}
```

# Break distance in x by pitch type and handedness (inches)

```
FF - R: [-10.53, -8.018, -5.445]	 L: [5.012, 7.962, 10.6795]
FT - R: [-16.521, -14.801, -12.843]	 L: [12.837, 14.692, 16.329]
SL - R: [0.981, 3.205, 5.76425]      L: [-5.383, -2.5555, -0.0785]
SI - R: [-17.03, -15.23, -13.26]	 L: [12.293, 14.275, 16.2185]
CH - R: [-15.846, -13.779, -11.342]	 L: [11.639, 14.168, 16.489]
CU - R: [3.972, 7.38, 10.689]	     L: [-9.04625, -5.0945, 1.63125]
FC - R: [-0.323, 1.743, 3.578]	     L: [-1.61375, -0.0105, 1.81175]
KC - R: [3.3485, 6.511, 9.582]	     L: [-4.694, -1.263, 2.051]
FS - R: [-13.1175, -10.544, -7.845]	 L: [-6.1205, -2.106, 2.3775]
```

# Break distance in z by pitch type (inches)

This includes the gravity Break

```
{'FF': [-15.3190, -13.2150, -11.2700],
 'SL': [-36.4580, -32.3560, -28.4820],
 'CH': [-30.8820, -27.4690, -24.2800],
 'FT': [-21.5690, -18.8820, -16.2360],
 'SI': [-23.7320, -20.4220, -17.4650],
 'KC': [-52.3893, -48.7220, -43.8212],
 'CU': [-53.9960, -48.6560, -43.5020],
 'FC': [-26.8620, -23.8000, -20.8100],
 'FS': [-32.6262, -29.4995, -26.2587]}
```

# How to use these values:

We will have an algorithm that picks end location and pitch time.

Starting location: just get average starting location by handedness

Pick vy0 by pitch type and pick average ay. This gives us `t`

Now get average break distance in x and z by pitch type and handedness

We will calculate `ax` and `az` such that `0.5*a*t*t` equalts the break distance

Now take the target location, subtract the break distances to get straight_x and straight_z

Use these to set vx0 and vz0.
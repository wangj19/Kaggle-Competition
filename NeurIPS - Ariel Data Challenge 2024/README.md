# [Competition](https://www.kaggle.com/competitions/ariel-data-challenge-2024)
## Overview
Are you ready to embark on a journey that pushes the boundaries of astronomical data analysis?

The Ariel Data Challenge 2024 invites you to develop machine learning models to solve one of the most formidable challenges in the field—extracting faint exoplanetary signals from simulated observations of the upcoming ESA Ariel Mission🚀!

## Description

The discovery of exoplanets—planets orbiting stars other than our Sun—has transformed our cosmic perspective, challenging conventional notions about Earth's uniqueness and the potential for life elsewhere. As of today, we are aware of over 5,600 exoplanets. Detecting these worlds is the initial step; we must also comprehend and characterise their nature by studying their atmospheres. In 2029, ESA Ariel Mission will conduct the first comprehensive study of 1,000 extrasolar planets in our galactic neighbourhood.

Observing these atmospheres is one of the hardest data-analysis problems in contemporary astronomy. When an exoplanet transits its host star in our line of sight, a tiny fraction of starlight (50–200 photons per million) passes through the planet's atmospheric annulus and interacts with its chemistry, clouds, and winds. These faint signals typically range from 50ppm (for Super-Earth like planets) to 200ppm (for Jupiter like planets) in magnitude and are regularly corrupted by the noise of the instrument.

The task of this competition is to extract the atmospheric spectra from each observation, with an estimate of its level of uncertainty. In order to obtain such a spectrum, we require the participant to detrend a large number of sequential 2D images of the spectral focal plane taken over several hours of observing the exoplanet as it eclipses its host star. Performing this detrending process to extract atmospheric spectra and their associated errorbars from raw observational data is a crucial and common prerequisite step for any modern astronomical instrument before the data can undergo scientific analysis.

# [Data](https://www.kaggle.com/competitions/ariel-data-challenge-2024/data)

Characterizing the chemistry of exoplanets is of the great active projects in astronomy. The European Space Agency's Atmospheric Remote-sensing Infrared Exoplanet Large-survey (ARIEL) mission will gather data on roughly 1,000 exoplanets by observing them while they transit in front of their host stars. Even with the powerful instruments on board ARIEL, the resulting data will be based on a limited number of photons and include a fair amount of noise. Your challenge in this competition is to extract the chemical spectrum of the atmospheres of exoplanets using simulated ARIEL data.

This competition uses a hidden test set. When your submitted notebook is scored, the actual test data (including a full length sample submission) will be made available to your notebook. Expect to see roughly 800 exoplanets in the hidden test set.

A dozen of the exoplanet simulations in the test set were based directly real exoplanets. All of those cases are ignored for scoring purposes.


# Solution
## Data Preprocessing
The dataset is super huge: every exoplanet has images captured by two instruments. AIRS-CH0 has 11250 rows of images captured at constant time steps noted in axis_info.parquet file for details of the time steps. Each 32 x 356 image has been flattened into 11392 columns. And FGS1 instrument has 135,000 rows of images at 0.1 second time steps for each planet. Each 32x32 image has been flattened into 1024 columns.

Since this competition requires super high professional knowledge, I've look through many EDA notebooks and hardly get helpful approach to summarize these huge datasets. Therefore I employ the preprocessing method that sums up flux of every image into a single number and records the flux change between images. Every exoplanet has an obscured period and the flux differences between obscured period and unobscured period of each exoplanet are used as features for wavelength prediction.

## Model
I currently used Ridge model since I only have 2 usable features so far.



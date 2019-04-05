# IEEE_Wavelets
Using Wavelets for incident detection and long term travel time forecasting.

## Introduction
This repository contains the code and paper to be presented at the Intelligent Transportation Systems Conference 2019.
All intellectual property here contained belongs to Alvaro Cabrejas Egea, the Centre for Complexity Science (University of Warwick) and The Alan Turing Institute.

## Goals
Take a dense time series of motorway travel times. 
Perform a continuous wavelet transform. 
Calculate the power of each frequency-time pair and identify outliers (median+iqr), set them to the maximum threshold, while the difference with this value is taken into the Spikes series.
Inverse transform both series, separating in this manner the recurrent from outstanding congestion.
Use this separated series to train a forecasting algorithm with 8 weeks of data and predict the following 4.
Assess the accuracy of the forecast, comparing with the published profiles and a null method.

## Contents
- Paper folder: Latex template with the written paper
- Code folder: Scripts used to obtain all graphs in the paper. These should be run in order.

## Running the code
1. Open R and Run 01Export_Link_to_CSV.R
  * Input : Clean Travel Time data
  * Output: 
    1. One CSV file per link containing the Travel Time
    2. Example plots of travel times
2. Open MATLAB and Run 02Separate_Background_Spikes.m
  * Input : One CSV per link containing Travel Time data
  * Output: Structured in a different folder per wavelet used
    1. Two CSV files per link. One containing the background and the other containing the Spikes
    2. One plot per link showing Original Travel Time and Reconstructed Series
    3. One plot per link showing the difference between Original and Reconstructed Series
3. Go back to R and run 03Profiles_calculation.R
  * Input : 
    1. Clean Travel Time Data
    2. Two CSV files per link. One containing the background and the other containing the Spikes
  * Output: 
    1. Plots for Mean Relative Absolute Error (MARE) across the times of the day in three flavors (Normal, Only Negative (Overprediction), Density Scaled)
    2. Plots for MARE or Root Mean Squared Error (RMSE) measured from quantiles 1, 95, 99, and a user defined one (default:50).
    3. Plots for the MARE as a timeseries for the 4 predicted weeks in three flavors (Normal, Only Negative (Overprediction), Density Scaled.
4. In R, run 04Plot_wavelet_decomposed.R
  * Input : 
    1. Clean Travel Time Data
    2. One CSV files per link containing the Background Series.
  * Output: 
    1. Spectrogram with timeseries data for the Original Travel Time
    2. Spectrogram of Wavelet Transform with timeseries data for the Background Series (Spikes identified and removed).
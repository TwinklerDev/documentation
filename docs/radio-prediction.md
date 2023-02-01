# 
# Radio Coverage Prediction

The goal of radio coverage prediction is to provide a good estimate of the radio signal power that will be received at points on the earth around a radio transmission from a single point. It must be noted that all radio coverage predictions are estimates only, and are limited by the accuracy of the geospatial data, the assumptions of whatever propagation model is selected and the additional parameters that are set.

# Prediction Framework

Twinkler provides a generic framework for radio coverage prediction that consists of three parts:
* Transmit System
* Radio Channel
* Receive System

![radio system](/_media/radio_system.png)

## Transmit System

The **Transmit System** consists of a *transmitter* that produces a modulated signal at a nominated power level (expressed in dBm). The signal consists of a range of frequencies (ie. its bandwidth) that is characterised by a center frequency. The signal is carried to an *antenna* that emits the power as radiowaves. The antenna is characterised by its pattern, which describes the strength of the radiowaves relative to each other in three dimensions around the antenna. There may also be be power *losses* in the transmit system eg. from cables and connectors.

## Radio Channel

The **Radio Channel** describes how the radio waves travel from the transmitting antenna to the receiving antenna. For coverage prediction it is most important to know how much of the power from the transmit antenna actually reaches the receive antenna. That is, how much power was "lost" in the radio channel.

Many models have been developed to answer this question. Each model is applicable to a range of frequency bands and technologies. Radio channel modelling is a complex area and is a subject of ongoing academic and commercial study.

Twinkler provides a propagation model and default set of parameters for some common frequency bands and technologies. This allows novice users to quickly get familiar with the interface, providing coverage predictions that may be regarded as reasonable at a high-level. The propagation model and parameters can be changed by radio engineers with more in-depth knowledge, to provide coverage predictions that are closer to measured values.

There are many factors that can, to a greater or lesser extent, contribute to a loss (attenuation) of signal power over the radio channel. The propagation models take some of these effects into into account, whilst others can be manually adjusted for in Twinkler.

* Building/Vehicle penetration loss
* Foliage/land-use loss
* Fading - shadowing, reflections etc
* Diffraction
* Rain/ice, oxygen absorption

*Margins* may also be added to account for other system-specific effects, or provide a greater level of confidence in the predicted coverage eg. interference.

Futhermore, there may also be some *gains* that result in more signal power arriving at the receiver than the propagation model alone would predict eg. from beamforming or upfade.

## Receive System

The **Receive System** is the reverse of the transmit system. Radio waves are received by the *antenna* and carried to the *receiver*, which demodulates the signal. The receive antenna also has a pattern that can cause a gain or loss of radio power. There may also be further *losses* in the system eg. body, cables and connectors.

## Edge of Coverage

In radio coverage prediction, the most important output is often the "edge of coverage". The end-to-end radio system should be taken into consideration when viewing or analysing the edge of coverage. For example the following questions should be answered:

* What type of transmitter and antenna was used?
* Were the margins and losses assumed to be conservative or optimistic?
* What receiving system was considered?
* What were the assumed receiving conditions? Indoors, hand-held etc

Moreover, all receivers have a minimum received signal power limit, below which they are unable to demodulate a signal. This limit is determined initially by theory but then modified by  factors such as the radio technology in use, and the design and quality of each type of receiver. This limit sets the maximum edge of coverage for a particular receiver. 


# Radio Technology

Different radio technologies characterise the radio channel in different ways. The notes below are a guide to some values that have been used in Twinkler for each radio technology. Users are encouraged to determine the planning values that are most suitable for their own needs through further reading and experimentation.

## 2G GSM

BCH RSSI as measured by the user equipment.

## 3G UMTS

CPICH RSCP as measured by the user equipment.

## 4G LTE

RSRP as measured by the user equipment.  

| Coverage Type | Configuration (W) | Bandwidth (MHz) | Tx Power per RSRE (dBm) |
| - | -: | -: | -: |
| Rural outdoors | 2x60 | 10 | 23 |
| Urban outdoors | 2x40 | 20 | 18.2 |
| Microcell | 5 | 10 | 9.2 |
| Picocell | 1 | 5 | 5.2 |
| Femtocell | 0.1 | 5 | -4.8 |

## 5G NR

SS-RSRP as measured by the user equipment.

## WiFi

RSSI as measured by the user equipment.


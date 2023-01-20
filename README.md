# ADSBfr24toOGN
Grab gliders with ADSB out from Flight Radar 24 and forward them to the OGN
  
  ## How it works
This script connects to an ADSB API (for ADSB positions) and the OGN (for FLARM positions). The script listens to both sources and manages a traffic list composed of each unique aircraft's position, speed, altitude, etc from both sources.

If a glider position exists from ADSB and not from FLARM, that glider's position is pushed to the OGN from the ADSB source with a 5 second interval.
If a glider position exists from both ADSB and FLARM, that glider's ADSB position will only be pushed to the OGN when the FLARM source is 120 seconds older than the ADSB source. Thereby seamlessly transitioning between the high refresh rate FLARM position and a lower refresh rate but larger ranged ADSB position.

To be seen, you will need to have a Mode S (non ADSB and be within MLAT range) or a Mode S ES (with ADSB) transponder. The script is set up to run on my pi from 9a to 8p MST, 7 days a week. And at the moment it is only set up to scan the North American lat/lon range.

The API is queried at 10 second intervals then the valid positions are sent to the OGN. For tracking, the signal has a refresh rate of somewhere between 5 and 15 seconds. A much lower resolution than the OGN's 1-2 second position intervals but ADSB has a much larger range.

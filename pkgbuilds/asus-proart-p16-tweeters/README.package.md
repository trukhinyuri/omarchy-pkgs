# asus-proart-p16-tweeters

The ASUS ProArt P16 H7607BA (NVIDIA N1x) has a 2-way speaker system: two woofers on Cirrus CS35L56 amplifiers and two tweeters on the Cirrus CS42L43's speaker amplifier. Omarchy's UCM profile for this laptop routes the tweeters from SoundWire port DP5, which also feeds the headphone output, and its speaker tuning sends the high band of the speaker signal there through a crossover.

This package mutes the tweeters (`cs42l43 Speaker Digital Switch`) while headphones are plugged in and unmutes them when they are pulled, following the codec's `Headphone Jack` control with `alsactl monitor`.

What it installs:

- `/usr/bin/asus-proart-p16-tweeters`
- `/usr/lib/systemd/system/asus-proart-p16-tweeters.service`, which runs only on board `H7607BA`
- `/usr/lib/udev/rules.d/70-asus-proart-p16-tweeters.rules`, which starts the service when the `mt8901soundwire` card appears

Based on the `proart-tweeter` user service of https://github.com/trukhinyuri/proart-p16-linux (Leon Marzoll, GPL-2.0-only), which also set PipeWire's default sink; on Omarchy WirePlumber and the speaker tuning handle that.

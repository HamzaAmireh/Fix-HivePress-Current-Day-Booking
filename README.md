# Fix-HivePress-Current-Day-Booking
This fix the ability for users to select the current day to make booking for WordPress HivePress Booking Feature

## 1- go to the /wp-content/plugins/hivepress-bookings/includes/components/class-booking.php

## 2- find

public function get_shifted_time( $listing, $time, $old_timezone = 'UTC' ) {
		// Check settings.
		if ( ! $this->is_time_enabled( $listing ) ) {
			return $time;
		}

## and change it to

public function get_shifted_time( $listing, $time, $old_timezone = 'UTC' ) {
		// Check settings.
		if ( ! $this->is_time_enabled( $listing ) ) {
			return $time >= time();
		}

## save and close.

## 3- go to /wp-content/plugins/hivepress-bookings/includes/controllers/class-booking.php

## 4- find

if ( $start_time && $end_time && $end_time >= $start_time && $start_time > hivepress()->booking->get_shifted_time( $listing, time() ) ) {

## and change it to

if ( $start_time && $end_time && $end_time >= $start_time && $start_time >= hivepress()->booking->get_shifted_time( $listing, time() ) ) {

## save and test your booking for current day and others

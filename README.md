# proje-ct-initial-code


#!/usr/bin/perl -w

use strict;
use Time::Local qw/ timelocal /;
use LWP::Simple;

my ( $currentDate, $endDate, $date_gen );
my $url_short = "http://www.bseindia.com/download/bhavcopy/Equity/EQ";

$currentDate = time();

#print "\nEnter the end date for the download string url: \n";

$endDate =shift(@ARGV);
#chomp($endDate);

if (not defined $endDate) {
die "Need end date....please enter it in ddmmyy format \n";
}




sub epoch_for_ddmmyyyy {
        my ($d, $m, $y) = unpack 'A2A2A4', shift;
        timelocal(0, 0, 0, $d, $m-1, $y);
}

$endDate = epoch_for_ddmmyyyy($endDate);

print "\nThe URLs are as follows : \n" ;
my $url_new;
for (my $i = $endDate; $i < $currentDate; $i += 86400){
        my ( $sec, $min, $hours, $mday, $mon, $year, $wday, $yday, $isdst ) = localtime($i);
                        $year = $year + 1900 - 2000;
                        $date_gen = sprintf "%02d%02d%02d" , $mday , $mon+1 , $year;

                        $url_new .= $url_short . $date_gen . "_CSV.ZIP"."\n";
}

print "\n$url_new";

open(FH,">sendoutput.txt");
print FH  "$url_new\n\n";
close (FH);

print "\n\n";

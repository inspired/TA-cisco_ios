1. %IOS_RESILIENCE-5-NON_CONSOLE_ACCESS: Non console configuration request denied for command "no secure boot-config "
 - Add to diag eventtype
2. Facility PIXM doesn't match because of PIX exclusion. We only want to exclude PIX, not PIXM.
3. cts role-based counters enable 
 - %$ VDC-1 %$ %CTS-6-CTS_RBACL_STAT_LOG: CTS ACE permit all log, Threshold exceeded: Hit count in 10s period = 4
 - *Jun 2 08:58:06.489: %C4K_IOSINTF-6-SGACLHIT: list deny_udp_src_port_log-30 Denied udp 24.0.0.23(100) -> 28.0.0.91(100), SGT8 DGT 12
 -  cts sxp log binding-changes ! Turns on logging for IP to SGT binding changes. 
 -  epm logging

suspend_until
=============

Script to suspend a system until a specific time.<BR><BR>

<h3>Usage</h3>
<pre>suspend_until HH:MM</pre>
Please note the time is in 24-hour time format, with ":" as a separator<BR><BR>
<BR>
<h3>Usage Examples</h3>
<BR>First, make sure the script is executable: <PRE>sudo chmod +x suspend_until</PRE>then either...<BR><BR>
<ol><li>Call directly to immediately suspend the system until a specific time: 
    <pre>suspend_until 07:00 </pre></li> 
<li>Schedule your PC to suspend and wake up at specific times using the systemd service and timer units. <BR>There are examples provided by this repo in the [systemd](./systemd) folder. </li></ol>


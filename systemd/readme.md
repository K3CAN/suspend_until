<h3>Using systemd</h3>

These systemd files include a template service unit and two example timer units.<BR>
To use them:
<ol><li>Either move the main script to <code>/usr/local/bin</code>, or update the service unit file to reflect the script's location.
<li>Copy the service unit into a systemd folder, such as <code>/etc/systemd/system</code>.
<li>Create the desired timer units (see below), then move the timer unit(s) into the same directory as the service file. 
<li>Enable the timer via <code>systemctl enable [name of timer unit]</code>
</ol>

<BR><h3>Explanation</h3> 
The service unit is “templated” meaning that systemd will create the actual unit file automatically based on the template.<BR><BR>
To run the service unit directly, we would need to supply an argument (the wake-up time) to it when we start it. We do this by inserting the argument after the @ in the unit name. <BR>To manually start the service to suspend immediately and wake up at 7am, we would call <code>systemctl start suspend_until@07:00.service</code> <BR>See how we included the argument (the time) right after that @?  To check the status of the service we need to supply the argument again so that systemd knows which version of the service we want to know the status of, like <code>systemctl status suspend_until@07:00.service</code>. 

To create the timers, 

<h3>Using systemd</h3>

These systemd files include a template service unit and two example timer units.<BR>
To use them:
<ol><li>Either move the main script to <code>/usr/local/bin</code>, or update the service unit file to reflect the script's location.
<li>Copy the service unit into a systemd folder, such as <code>/etc/systemd/system</code>.
<li>Create the desired timer units (see below), then move the timer unit(s) into the same directory as the service file. 
<li>Enable the timer via <code>systemctl enable [name of timer unit]</code>
</ol>

<BR><h3>Explanation</h3> 
The service unit is a “template” meaning that systemd will create the actual unit file automatically based on the template.<BR><BR>
To run the service unit directly, we would need to supply an argument (the wake-up time) to it when we start it. We do this by inserting the argument after the @ in the unit name. <BR>To manually start the service to suspend immediately and wake up at 7am, we would call <code>systemctl start suspend_until@07:00.service</code> <BR>See how we included the argument (the time) right after that @? To check the status of the service we need to supply the argument again so that systemd knows which version of the service we want to know the status of, like <code>systemctl status suspend_until@07:00.service</code>. 

To create the timers, we need only a few lines of text in a <code>.timer</code> unit file. 

<code>[Unit]
Description=
</code>
Is just a quick reminder to the user (us) what this timer is for. It’s technically optional, but helpful.  

<code>[Timer]
OnCalendar=
</code>
Tells systemd when to trigger the service. In this case, then means when we want to the system to go into a suspend state.  

<code>[Install]
WantedBy=timers.target
</code>
Is the final line, which tells which <code>.target</code> unit wants this timer. Unless you have a reason to change it, <code>timers.target</code> is a sensible choice. 
<BR><BR>
The final, and VERY important bit of data is the <b>name</b> of the timer unit. 
You can see in the examples, the first part of the file name (before the @) matches the service. This is how systemd knows which timer belongs to which service. The second part is actually an argument we need to provide to the service.  Yes, there’s actually data <i>in</i> the file name itself!  In this case, that data is when we want the system to wake up from the suspend state. 

Putting it all together, we set the time we want to to put the system to sleep after <code>OnCalendar</code> in the timer file, and we put the time we want it to wake back up in the timer’s file’s <i>name</i>.   

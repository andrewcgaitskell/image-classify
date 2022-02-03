https://serverspace.io/support/help/vnc-connection-ssh-tunnel-ubuntu-20-04/

We recently covered the process of installing and configuring a TightVNC server on Ubuntu 20.04. In addition to this, the process of setting up a secure SSH tunnel for a VNC connection will now be described. This is because VNC itself is not secure. Using an SSH tunnel corrects the situation.

Cloud ServersIntel Xeon Gold 6254 3.1 GHz CPU, SLA 99,9%, 100 Mbps channelfrom4 EUR/month

# Preparation

In the first part, we opened firewall port 5901. The connection will now be directed through the SSH tunnel, so you need to close the ports open for VNC.

ufw deny 5901/tcp

You also need to close all running TightVNC sessions.

vncserver -kill :1

And start a session listening only for internal connections. After opening the SSH tunnel, this will be our connection.

vncserver -localhost

If you have configured the TightVNC service, open its configuration.

nano /etc/systemd/system/vncserver.service

Find the ExecStart parameter and make it look like this:

ExecStart=/usr/bin/vncserver -localhost

Reload systemd:

systemctl daemon-reload

And start (or restart) the service:

systemctl enable --now vncserver

Creating a SSH Tunnel

The following command must be run on the client computer from which you are connecting to the VNC server. It connects port 61000 on the local machine to port 5901 on the server via an SSH tunnel.

ssh -L 61000:localhost:5901 -N -l username VNC_server_IP

The following options are used to create a tunnel:

    -L - forwarding information from local port 61000 to remote port 5901 via SSH tunnel;
    -N - specifies to only forward ports, not execute the command;
    -l - specifies the username to create the tunnel.

Replace username and VNC_server_IP with your own parameters. If you connect using an SSH key, do not forget to add the -i parameter, as with a usual SSH connection.
Using Putty to create a SSH tunnel

Use normal connection parameters in Putty. Besides these, you need to add some settings. Namely, go to Connection - SSH - Tunnels, enter 61000 in the Source port and localhost:5901 in the Destination.

Click Add and Apply.

Connecting to a remote desktop

The tunnel has now been created.
To connect to the remote desktop, use the same client as in the first part of the tutorial - any VNC client you like.

Enter localhost:61000 as the VNC server.

# install gnome-remote-desktop

sudo apt install gnome-remote-desktop

# start gnome-remote-desktop

systemctl --user enable gnome-remote-desktop.service
systemctl --user start gnome-remote-desktop.service

# configure remote desktop

        gsettings set org.gnome.desktop.remote-desktop.vnc auth-method 'password'
        gsettings set org.gnome.desktop.remote-desktop.vnc view-only false

# install pass

sudo apt-get install pass gnupg2

# create a gpg2 key
gpg2 --gen-key

# create the password store using the gpg user id
pass init $gpg_id

dbus-launch echo -n 'password' | secret-tool store --label="GNOME Remote Desktop VNC password" "xdg:schema" "org.gnome.RemoteDesktop.VncPassword"
 
sudo dbus-launch secret-tool store --label="GNOME Remote Desktop VNC password" "xdg:schema" "org.gnome.RemoteDesktop.VncPassword"
 
systemctl --user start gnome-remote-desktop.service

loginctl unlock-session $(loginctl --no-legend --value list-sessions | awk '/seat/ { print $1}')


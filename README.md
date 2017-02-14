# PVE Snap

`pvesnap` is a tool to automate proxmox container snapshot and is supposed to be run
in a cron job.

# Author

Michaël Hauspie <http://cristal.univ-lille.fr/~hauspie>

# Configuration

As of today, the configuration can only be done by modifying the 
three variables at the head of the script:

* `MAX_SNAP_COUNT`: the maximum number of snapshot to keep **including** the one that will be created.
  This value is **per** container,
* `NODES_TO_SNAP`: an array that can either be empty or be a list of the VMID to snapshot. 
  If empty, snapshots are made for all containers,
* `SNAP_PREFIX`: the prefix used to identify snapshots managed by this script. The created snapshots
  will be named by concatenating this value to a timestamp (number of second since epoch is used as the t  imestamp)


# Cron setup

The easiest way to set the cron job is to put this script in
`/etc/cron.daily` to get snapshots every day. You can of course use
a cron script in `/etc/cron.d` or any `crontab` to get more control.

The only thing to remember is that a new snapshot is created at each call of
the script.  As the timestamp consist of a number of seconds, to consecutive
snapshots within the same second will fail. Given the time needed to make a
snapshot it is not likely to occur.

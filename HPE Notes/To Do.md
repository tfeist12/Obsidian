**Week of 6/30/25:**

In Progress:
- Update nvim config and push to repo
- Check on goals
- Make story for updating the kubectl dsp plugin.
- Review has been posted for the switch controller webhook changes
- Once this is complete I can start putting it all together
- Need to take a look at more bugs after this

Complete:
- Checked in the cli user rbac permissions for oncs P0 bug fix
- Renewed Virtual Digital Badge
- Finished writing webhook unit tests
- Check in with DSCC folks about switch port name field change
	- Need to provide the build number of this R3 change
- Pushed switch port name change
- Pushed switch firmware crd update and fake reconcile loop

[AS-197203](https://jira.storage.hpecorp.net/browse/AS-197203)
	Switch Firmware update steps:
		1. Set Offline request api -> OFF
		2. Upload firmware request api
		3. Reboot switch request api
		4. Set Offline request api -> ON
	Requirements:
	- Switchd to report if firmware version has been uploaded to the inactive partition ([AS-189429](https://jira.storage.hpecorp.net/browse/AS-189429 "Provide FW version for the secondary partition in ListSwitches/\"show switch\"")) or use a fixed wait time after which we assume the upload is complete.
	- Switchd GRPC client updates
	- State machine
	- Unit test updates

Update notes:
- Potentially use a mutating webhook that runs on create and update to populate spec fields
- This could render the creation reconciliation operation obsolete


 delete mode 100644 Obsidian/HPE Notes/Docker.md
 delete mode 100644 Obsidian/HPE Notes/Git.md
 delete mode 100644 Obsidian/HPE Notes/Golang.md
 delete mode 100644 Obsidian/HPE Notes/Intern Coordinator/2022/Community Service Email Draft.md
 delete mode 100644 Obsidian/HPE Notes/Intern Coordinator/2022/Community Service.md
 delete mode 100644 Obsidian/HPE Notes/Intern Coordinator/2022/End of Summer Celebration.md
 delete mode 100644 Obsidian/HPE Notes/Intern Coordinator/2022/Mentorship Week 1.md
 delete mode 100644 Obsidian/HPE Notes/Intern Coordinator/2022/Mentorship Week 2.md
 delete mode 100644 Obsidian/HPE Notes/Intern Coordinator/2022/Welcome Picnic.md
 delete mode 100644 Obsidian/HPE Notes/K9/Daily Scrum/2024/01-10.md
 delete mode 100644 Obsidian/HPE Notes/K9/Daily Scrum/2024/01-16.md
 delete mode 100644 Obsidian/HPE Notes/K9/Daily Scrum/2024/01-17.md
 delete mode 100644 Obsidian/HPE Notes/K9/Daily Scrum/2024/01-30.md
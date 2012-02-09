==================================================
# Dead Man's Switch for Android #
==================================================
Work on this project has only just begun, and anyone who feels up for the
challenge is more than welcome to help out. 

The design concept thus far is to create a traditional [Dead Man's 
Switch](https://en.wikipedia.org/wiki/Dead_man%27s_switch),
for which the user will be capable of choosing the amount of time before
the switch is activated and the preconfigured actions are executed 
automatically by the program. Implementation features for configurable
executable actions should include tasks like deleting the Contact List on
the user's phone, deleting emails (either on the phone or through ssh on
a remote server), deleting all contents of a remote server (or shutting
it down in the case of a remote server with full-disk encryption which
has sensitive information). Features should be added depending on what
activists will need from a Dead Man's Switch in the event of arrest or
incapacitation.

It was discussed among the developers involved with [March Hare 
Communications Collective](http://comms.hackbloc.org/) that, in the 
United States, activists' phones are often imaged upon intake to jail 
or other "correctional" facilities, which requires the phone to be shut 
down. This creates problems for the design implementation in this 
application, because, in the event that the user's phone is turned off, 
the Dead Man's Switch would be unable to execute the specified tasks. 
The only way I can imagine getting around this is to set up a server 
somewhere, which stores a set of actions to be taken in the event that 
the user's phone does not contact the server to postpone events within 
the set ammount of time. A useful thing to do with this as well would be 
to have the application tell the phone to send out a 
zomg-my-phone-is-dying message when the battery reaches a critical level, 
so that the user's affinity group at least has some information that the 
Dead Man's Switch may have been triggered due to the user's phone being 
dead.

## Software Requirement Specifications ##

### Functionality ###
* _Timer function_. Should deploy preconfigurable actions without user input, and require user input only to prevent actions from occurring. The amount of time before the switch goes off should be user configurable. Also, the user should be prompted for a passphrase to deactivate the switch, so that captors of, or antagonists to, the user cannot delay or disable the preconfigured actions.
* _Preconfigurable actions_. Desired actions thus far include deleting contacts lists, SMSs, emails, and other phone data, deleting contents of or shutting down a remote server, sending forth an army of robot minions to spring the user from jail. If you can think of a useful action, _please_ [submit a feature request to the developer](mailto: isis@hackbloc.org). 
* _Backend services for server_. In the event that the phone is powered off, [as is often the case when a phone is taken for forensics imaging](http://techno-forensics.com/article/examining-cellular-phones-and-handheld-devices), it would be convenient for the Dead Man's Switch application to actually store the timer function and preconfigurable actions on a remote server, if possible, in order that they are executed regardless of phone state. Obviously, in this situation, preconfigurable actions to modify data on the phone itself become unexecutable.
* _Low power emergency actions_. The application should be able to read the phone's battery level to determine if the phone is dying. If the phone is dying, the application should perhaps execute a _different_ set of preconfigured actions, such as sending SMSs to members of the affinity group to notify them that the user is still active but that their phone is dying.
* _Unexpected power off actions_. If the phone is unexpectedly powered down while battery levels are still sufficient, and a backend server has been configured, we should determine if there is a method for the phone to send a last minute panic message to the server. This is probably not feasible, however.

### External Interfaces ###
* _Visibility_. The application should attempt to hide itself in the background, similarly to the OpenWatch app, i.e. there should not be any icons in the action bar showing that the app is running. The app should be visible only during configuration and when the timer has gone off.
* _Hardware Interfaces_. 3/4G connection, wireless connection, access/modify SD Card contents.

### Performance ###
* _Speed_. The Dead Man's Switch application should avoid unnecessary drains on system resources.

### Attributes ###
* _Portability_. A [sister app](https://github.com/March-hare/DeadmansSwitch_Iphone) is being designed for iPhone devices. There are no current plans to offer the application on either Symbian or Blackberry. Only feds and CEOs use Blackberries anyway.
* _Correctness_. We intend to be politically correct. That's what we're supposed to say at this part of the Software Requirement Specification, right, IEEE?
* _Maintainability_. Classes should be designed in a modular fashion so that they may be easily updated. Strings, where possible, should be kept in a separate .xml file, so that the application is easily translatable to other languages. Document anything that looks wonky, which is really all of it, since it's Java for christsakes.
* _Security_. Where possible, all stored data should be encrypted with passphrase protection. MD5 is not acceptable for hashes, only SHA-256 or SHA-512. Communication with networked services should never be plaintext. This application should not expose the user to any further attack surface than would already be available were it not installed.

### Design Constraints ###
* _Language_. Java. Yes, it sucks.
* _Platform_. Android 2.3.3+
* _Feature Freeze_. Starts on April 30th, 2012.
2.9.0 16/08/2023
================
 * Fix instance activity to register keyboard
 * Add daily job to remove instance activity data older than configured age (env var VISA_INSTANCE_ACTIVITY_RETENTION_PERIOD_DAYS)
 * Remove duplicates of cloud security groups
 * Allow security groups to be applied to specific flavours

2.8.1 10/05/2023
================
 * Fix anonymous access to /api/jupyter/instances/{instance}/notebook/close
 * Fix null pointer exception creating security groups.
 * Modify create/delete test scripts: assume that the token already includes the prefix "Bearer "

2.8.0 28/04/2023
================
 * Minor updates to standardise the API 

2.7.1 21/04/2023
================
 * Fix bug on role based security groups SQL

2.7.0 20/04/2023
================
 * Soft deletion of plans
 * User groups: allow groups of users to be created by admin. Groups work the same as roles and can be used in the management of flavours and security groups.

2.6.0 21/03/2023
================
 * Ensure instance expirations are removed when an instance termination date is set to null (immortal)
 * Add role-based flavour limits (flavour only available to users with specified roles)
 * Add WebX as a remote desktop implementation (some features unavailable such as instance sharing and screen capture)
 * Refactor remote desktop to add abstraction layer to implementation

2.5.1 23/01/2023
================
 * Fix tests
 * Fix bug on experiment search failing when ordering by instrument or proposal identifier.

2.5.0 20/12/2022
================
 * Check whether visa is in open-data mode before sending back all the members of the proposals: empty the list of the user is not part of the original proposal.

2.4.4 22/11/2022
================
 * Fix bug on creation of instances with open data (experiment check takes into account open data)

2.4.3 21/11/2022
================
 * Add env var (VISA_INSTANCE_USER_DEFAULT_QUOTA) to allow configuration of default instance quota for users created by VISA

2.4.2 18/11/2022
================
 * Add possibility to search for open data (disabled by default, enabled with env var VISA_CLIENT_CONFIG_INCLUDE_OPEN_DATA)
 * Allow protocols to be optional (allow remote desktop to be available before Jupyter starts)
 * Change default SSO scope (remove offline_access)

2.4.1 15/11/2022
================
 * Add url and doi columns to experiment and proposal tables
 * Filter by DOIs or Proposal Identifiers when getting experiments for a user 

2.4.0 24/10/2022
================
 * Record mouse and keyboard activity on instances to maintain history of when users have interacted with instances
 * Allow users to indicate whether others can access their instance when they are not connected
 * Allow for multiple cloud providers: Cloud providers can be configured from database settings as well as the default config file
 
2.3.2 23/09/2022
================
 * CC the admins in the email sent when replying to instance extension requests (keep all team informed)
 * Allow experiments to have specific titles (different to proposal titles): use proposal title by default
 
2.3.1 08/09/2022
================
 * Use a separate email address for the instance creation emails (env var VISA_NOTIFICATION_EMAIL_ADAPTER_DEV_EMAIL_ADDRESS) 
 
2.3.0 01/09/2022
================
 * Filtering of experiments that don't have valid start or end dates
 * Add admin notifications (currently for instances in error and instance extension requests) shown in admin UI
 * Add endpoints to handle instance lifetime extension requests and email templates for the extension request workflow
 * Add GUEST role and expiration date to role (provides time limited access to VISA to users that aren't associated to proposals)
 * Add health check endpoint for use by application credentials
 * Authentication via application credentials - can access specific API endpoints using basic auth. Endpoint to manage app credentials.

2.2.1 09/05/2022
================
 * Fix bug on notification service throwing an error when an adapter is not enabled

2.2.0 23/03/2022
================
 * Update the instance creation and deletion scripts (used for testing cloud providers)
 * Add database migration scripts for use with dbmate (include in Docker container too)
 * Fix some OpenStack issues by accepting case-insensitive headers
 * Modify system notifications to allow them to be re-used (activate/deactivate) and soft delete
 * Add UID to Instance model to be used in client routes and server REST API
 * Update library dependencies
 * Fix email template typo
 * Ensure HTTP client requests and responses are closed correctly

2.1.1 26/11/2021
================
 *  Catch 401 errors from the account service and log accordingly (don't log as an error).

2.1.0 17/11/2021
================
 * Update configuration for openid connect
 * Fix issue with log level set to debug
 * Filter experiments by start date only
 * Create users automatically if they do not exist in the database 
 * Allow for empty analytics configuration
 * Update persistence XML files to conform to JPA schema 2.2

2.0.2 30/09/2021
================
 * Add Web Cloud Provider (cloud instances managed through a middleware)
 * Add graphQL endpoints for security group, security group filters and flavour limit management
 * Remove Cycle table and all references
 * Add errors to payload of paginated responses
 * Allow for searching of experiments by proposal Id
 * Add user role management admin UI

2.0.1 30/07/2021
================
 * Set activated and update lastSeenAt when users access visa
 * Fix bug on experiment count criteria builder
 * Add graphql endpoint to update instance termination date
 * Add graphql endpoints for jupyter session stats
 * Upgrade to guice 4.2.3: better error handling on startup
 * Send VISA PAM public key as metadata to instance
 * Fix email template env vars
 * Fix instance expiration bug: check for deleted instances correctly
 * Fix environment variable names

2.0.0 15/06/2021
==============
 * VISA platform open sourced and moved to GitHub
 * Updated docker build
 * Add autologin to images (optional use of visa pam module)  
 * Enable/disable admin emails
 * Explicit naming of foreign keys, unique keys and constraints
 * Searching for experiments using dates rather than cycles
 * Email template directory configuration
 * Add instance attributes table and pass to openstack 
 * Migrate Instrument Responsible to Instrument Scientist
 * Use VISA Accounts micro-service for authentication
 * Convert many database booleans to timestamps (eg instance deleted_at)
 * Add summary to proposal
 * Remove dependency on Cycle in business logic (eg instrument control support user)  
 * Add start and end date to ExperimentF
 * Use Security Group Service to determine instance security groups (logic removed from API Server)
 * Make user IDs strings rather than longs

---

1.0.23 30/04/2021
=================
 * Add keyboard_layout to instances
 * Fix bug on integer overflow for instance session durations
 * Add deleted_at date to instances
 * Hide plans that have deleted flavours

1.0.22 22/01/2021
=================
 * Added Configuration table/entity (and repository + service) for dynamic server configuration
 * Filter security groups by role for staff when creating instances
 * Increase inactivity duration for staff to 8 days (keep 4 days for non-staff)

1.0.21 13/01/2021
=================
 * Modified account instances endpoint to enable filtering of instances by experiments or roles
 * Added allowedRemoteClipboardUrlHosts to configuration to allow client to suggest opening URLs in another tab when copied to clipboard in instance
 * Soft delete flavours
 * Send list of experiments and instruments to instances (openstack parameters) for future module env
 * Fix bug on jupyter session database entries

1.0.20 30/11/2020
=================
 * Upgraded guacamole library
 * Specifying guacd options inside configuration (i.e. ignore-certs and rdp port)
 * Added username and home directory to graphql types

1.0.19 19/11/2020
=================
 * Fix hibernate problems: always obtain the latest instance object from the DB rather than using the session version.

1.0.18 13/11/2020
=================
 * Filter plans by user and experiments: allow IRs on selected instruments to access to large flavour automatically 
 * Change instance lifetime to 60 days for staff
 * Allow only owners to access Jupyter notebooks
 * Sort proposed plans by flavour
 * Added a preset to the plan to provide default image+flavour to users

1.0.17 26/10/2020
=================
 * Modify openstack instance cleanup code to remove all zombie instances
 * Add scientific computing role (available as a scientific support user on instance members UI)
 * Add instance jupyter session data for statistical analysis of jupyter usage in visa
 * Add endpoints to be used by visa-jupyter-proxy (keepalive and session data)
 * Use image protocol service to associate ports to an image (remove hardcoding and allow for jupyter notebook to be activated dynamically)
 * Store the instance IP address in the instance table
 * Send instance ID and user home directory as metadata to openstack when creating the instance

1.0.16 03/09/2020
================
 * Add Employer model as affiliation to User rather than simple string name for better stats
 * Get all support users rather than staff for instance support members
 * Change instance handling in actions to avoid transaction problems
 * Increase max frame payload length to 200KB to avoid exceptions on large thumbnails 
 * Catch exceptions when sending emails for expiration notifications 
 * Allow instrument responsible and admin users to connect using the support page to external user instances when the owner is disconnected.

1.0.15 25/08/2020
================
 * Storing thumbnails as base64 instead of blobs
 * Added system notification graphql endpoints
 * Reduce race conditions on instance states by executing commands on a single load balanced server

1.0.14 18/08/2020
================
 * Add cloud instance cleanup job
 * Ordering of cycles by most recent
 * Modify logging of connected user and users
 * Added thumbnail upload over websocket
 * Remove name and description from Plan
 * Log and create error if userId equal to 0
 * JProfiler checks: make repositories and services singletons

1.0.13 15/08/2020
================
 * Use socket.io ping configuration
 * Add graphql endpoint to get interactive sessions
 * Add more instance information to remote desktop logs

1.0.12 14/08/2020
================
 * Handle deletion of instances while they are stopping
 * Fix date format for Safari
 * Added analytics information to client configuration
 * Added lastInteractionAt to InstanceSessionMember

1.0.11 13/08/2020
================
 * Fix guacd timed out problem using socketio pings to detect client socket closure.

1.0.10 11/08/2020
================
 * Add graphql endpoint for recently active users
 * Update delete instance mutation in graphql
 * Send instance lastInteractionAt to clients
 * Fix gitlab CI

1.0.9 10/08/2020
================
 * Fix date format problem for graphql types
 * Add lastInteractionAt to instance to determine when last mouse or keyboard event was made
 * add endpoint to get user by last name 
 * Change dashboard to show number of images and flavours in use by the instances
 * Reduce log to warn for unauthorized access to a remote desktop
 * Add active sessions to instance resolver
 * Extra logging on command execution

1.0.8 09/08/2020
================
 * Fix mapping of users of experimental team
 * Get sessions for individual instances
 * Fix syslog config
 * Change sql request for instrument control support users' instances (get all instances with experiments in a 7 day window)
 * Improved error logging and emails
 * Add hikari database connection pool

1.0.7 06/08/2020
================
 * Increase request timeout to OpenStack API
 * Close access request modal on owner's machine when user cancels request (multi server env ok)
 * Bug fix: Handle multiple current sessions for an instance
 * Add instance quota to users
 * Scripts for creating and deleting instances (for OpenStack perf testing)
 * Extra information in error logs
 * Graceful deletion of instances: shutdown first
 * Add boot command to Image and sent it to an instance when it is created
 * Send metadata (owner username) to OpenStack on instance creation

1.0.6 04/08/2020
================
 * Added gitlab CI for docker image creation
 * Add file appender and syslog appender
 * Get only active plans for admin interface
 * Soft delete sessions and session members when deleting an instance 
 * Add 1 week before and after cycle for security group management to allow access to instruments during this period 
 * Add random name generator
 * Send emails to members when they are added to an instance
 * Add email appender to send emails when an error log message occurs 
 * Improve logging details (including user and instance IDs)
 * Added last seen at to users for statistics 

1.0.5 23/07/2020
================
 * Allow the owner to disconnect specific clients from an active desktop session
 * Endpoint to return active sessions for an instance
 * Add version number to image
 * Remove stale sessions on server startup
 * Option to change access to read-only when the owner disconnects (room locked) rather than disconnecting all other clients
 * Handle read-only access to desktops using the 'display' event listener (drop keyboard and mouse events)
 * Notify clients when access has been granted by owner to share their desktop
 * Fix bug on instance expirations not being deleted if instance is deleted manually first

1.0.4 20/07/2020
================
 * Desktop access requests for dynamic access to remote desktops for support users (messaging to owner for explicit access grants when support user wants to connect), multi-server model ok
 * Obtain list of instances for the different support roles with filtering
 * Add different support roles (instrument control, IT support  and instrument responsible)

1.0.3 13/07/2020
================
 * Bug fix: change url to get support users

1.0.2 10/07/2020
================
 * Get instances for instrument control support
 * Mapping instrument responsibles
 * Added system notifications

1.0.1 09/07/2020
================
 * Change ScientificSupport role to Staff role and remove automatic access to instances (used for security groups)
 * GraphQL session endpoints

1.0.0 07/07/2020
================
 * Server client configuration data to determine server version and keycloak information (avoids multiple environments for client, facilitates docker config)
 * Add protocols to image update in graphql
 * Docker configuration
 * Bug fix: remove cascade of updating images when saving instances (remove also instance object from remote desktop connection session data)
 * Add activated flag to users to determine which ones have connected at least once to visa
 * Add plans to graphql
 * Add owner username to instance to allow for connections when owner is absent
 * OpenStack security groups managed purely through database entries (remove from config)
 * Store session connection history in database
 * Load-balancing of desktop connections using a redis server

#9062490 18/06/2020
===================

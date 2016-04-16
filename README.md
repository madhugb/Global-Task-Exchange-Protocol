# Global-Task-Exchange-Protocol
---

Task management systems are invariably creating one of many data silos. If we take an example of email, it reflected the real life behaviour of `postcard` and made it available to everyone. Calendar protocol reflected the real life invitations to events. But for tasks we are still dependent on Emails, Calendars, or some task management softwares.

Now these task management solutions work beautifully inside a wall. It fails when the task is shared between 2 different entities.

So, What if anyone is able to assign a task to anyone else, just like an e-mail system.
---

##Proposal

Here is what I am proposing. Every domain gets  set of TX records (like MX records). These indicates the server where the tasks are stored, and bunch of other settings.

The hierarchy looks like this.

	Domain

		User

			Project

				Task


*Task* is owned by a Project. *Project* belongs to a User. *User* is a member of Domain.

###Domains

- Domain is identified by Canonical Names of the hosted server.
- For example `example.com`, `tasks.example.com`

###Projects

- A project is like a folder to keep set of tasks.
- Project is identified by an id and name
- Project id is `<unique-id>@<domain-name>`.
- It exists somewhere in
	`/var/spool/tasks/<my-domain>/<my-email>/projects/<project-domain>/<project-id>/`

###Tasks

- Tasks are documents containing information and history of the work
- A task must belong to a project.
- ID of the task must be globally unique and it should end with project id `<uuid>-<project-id>@<domain-name>`

###Members

- Users identified by Email address
- Every member has a role [CREATOR, OWNER, GUEST etc ]
- Every member can have a default project by their email address (which will be unique of course) which acts as a personal todo.



The system is not truly distributed. Even though every member will have a copy of it (depending on scope and role), it has a master copy which belongs to the creator of the project (just like calendar).

Some more info

- Any change in the task is synced back to the master copy.

- Any change is recorded as history and can be reversed just like Git.

- Task is a multipart document, which means it supports attachments and custom fields

Now here are some questions.

####How do I trust if the other guy / system is legit?

Use private and public keys encryption

####How to sync/patch updates? conflicts?

It looks like git is already solving this :-)

####Who should be able to assign me a task?

Actually it is like Email, anyone can assign you a task. However you can block or ignore the requests.

## The MIT License (MIT)

See [License.md](https://github.com/madhugb/Global-Task-Exchange-Protocol/blob/master/LICENSE.md)

## Author

[Madhu Geejagaru Balakrishna](https://twitter.com/madospace "Follow @madospace on Twitter")

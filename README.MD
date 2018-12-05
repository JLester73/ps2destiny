**NOTICE**
These files and scripts are provided without any assurances that they
will work properly in your environment.  There is also no guarantee
that something won't get messed up in either PowerSchool or Destiny
by using this project.  Use at your own risk, understand what the
commands will be doing, and use in a test environment if possible!

**Background**
This program was created by Jason Lester of Washingon County Schools.

**Description**
These scripts export out students, teachers, and sections from PowerSchool
that are needed for import into Follett Destiny Library Manager and Resource
Manager.  There are lots of moving parts to this and various pieces that
run in PowerSchool, scripts that run on a PowerSchool application node,
and scripts that run on a Linux server.

**Release**
The latest version is always available on Github from:
  https://github.com/JLester73/ps2destiny
  
**Setup**
Setup to make all this work requires admin access to PowerSchool, console
access to at least one of your PowerSchool application nodes, and access
to a Linux (or other) server that can run Ruby scripts

- The /autosends folder contains the information you need to setup the
  required Autosends in PowerSchool.  Students.autosend and Teachers.autosend
  are both setup in your "District Office" school so that they have access to
  all students and teachers.  Sections.autosend must be setup for each school
  so that it will have access to the individual sections.  Just paste the
  contents into the Fields to Export field.  Students and Teachers just write
  out to the default autosends folder for your PowerSchool share.  Sections
  writes out to a managed remote connection on the server that will run the
  Ruby script.
- The properties/ folder contains the .properties files required by the
  Destiny Importer Converter.  There is one for students, for class imports,
  one for updateclasses, and two for teachers.  The reason for the two teachers
  setup is because of the differing ways that PowerSchool and Destiny handle
  inactive/deleted teachers.  One updates teachers and then the other runs to
  delete teachers who are inactive.  The .properties files are all setup to
  use the Autosend jobs set up previous in PowerSchool.  If you change any fields
  in the Autosends, you also need to update your properties files.
- The scipts/ folder contains the batch files and shell script used to run
  everything. The batch files all run on a PowerSchool application node that
  has the Destiny Import Converter loaded along with the properties/ files
  above.  Change the paths as appopriate.  The ps2destiny shell script runs
  on the Linux server to fix the sections into the format Destiny wants.

**Usage**
- Set your Autosends to run at a certain time each night.  We use roughly
  10:00 PM for everything.
- Set a cron job on your Linux server to run the Ruby script to modify the
  sections.csv file.
- Setup scheduled tasks on your PowerSchool application node to run the
  converters for students, teachers, teachers_delete, and courses.

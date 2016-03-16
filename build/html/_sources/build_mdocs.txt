####################
Build & Deploy mDocs
####################

Generally speaking, here's what you need to know about mDocs:

+----------------------+---------------------------------+------------------------------------------------------------------------------+
| Item                 | Description                     | Location                                                                     |	
+======================+=================================+==============================================================================+
| Source files         | Version controlled using Git    | `mdocs-flare-source                                                          |
|                      | Hosted on Github                | <https://github.com/Mozu/mdocs-flare-source>`_                               |
+----------------------+---------------------------------+------------------------------------------------------------------------------+
| Compiled output      | Version controlled using Git    | `Mozu.AuthContent                                                            |
|                      | Hosted on internal TFS server   | <http://tfs.corp.volusion.com:8080/tfs/vnext/v2Mozu/_git/Mozu.AuthContent>`_ |
+----------------------+---------------------------------+------------------------------------------------------------------------------+
| Automation           | We use a batch file to automate | `mdocs                                                                       |
|                      | the build and deploy processes  | <https://github.com/Mozu/mdocs>`_                                            |
+----------------------+---------------------------------+------------------------------------------------------------------------------+

This is the workflow:

	#. Create/edit source content
	#. Build local output
	#. Publish local output
	#. Deploy local output to a MicroDev environment for review
	#. Deploy local output to production

Before you begin, make sure you've set up your development environment.

	- Git
	- posh Git
	- SSH Keys
	- SSH Agent
	- Difftool
	- Text editor

**************************
Create/Edit Source Content
**************************

Under normal circumstances, we follow the Git flow process to create and deploy documentation. Feature branches represent documentation changes. You should also use feature branches for substantial changes that result from backlog work items. For minor changes, you can make changes directly to the ``develop`` branch.

	#. Clone the `mdocs-flare-source <https://github.com/mozu/mdocs-flare-source>`_ repo.
	#. Open a terminal and navigate to the cloned repo.
	#. ``git flow feature start <my-feature>``
	#. Create, revise, or delete content.
	#. Build local output to verify format and layout.
		
		#. Run the ``build_mdocs.bat`` file.
		#. Select option **1** or **2**.
		#. View the output.
		
	#. Deploy output to a MicroDev environment for stakeholder review.
	#. Notify stakeholders that content is ready for review.
	#. Revise content if necessary.
	#. Coordinate with team before running feature complete commands.

******************
Build Local Output
******************

Both mDocs and API build to different output locations that need to be merged into a single location. The ``build_mdocs.bat`` script automates the build and merge process.

To run the script:

	#. Clone the `mdocs <https://github.com/mozu/mdocs>`_ repo.
	#. Navigate to ``mdocs/batch file source``.
	#. Copy ``build_mdocs_source.bat`` to the ``mdocs`` directory and rename it ``build_mdocs.bat`` (ignored by git). 
	#. Open ``build_mdocs.bat`` in a text editor.
	#. Configure the variables at the top of the file to match the directory paths on you local machine.
	#. Save and close the file.

To build local output:

	#. Run ``./build_mdocs.bat``.
	#. Select option **1** or **2**.
	#. View content at ``C:/mdocs/publish/index.htm``.

********************
Publish Local Output
********************

Publishing refers to the process of copying the merged ``mDocs`` and ``API`` output to the ``Mozu.AuthContent repo``. We've automated this process using Gulp and the batch file. Option **3** in the ``build_mdocs.bat`` script publishes local output. Refer to the next section for an example.


****************************************
Deploy Content to a MicroDev Environment
****************************************

**Note:** You must first create a remote branch in the ``Mozu.AuthContent`` repo for the MicroDev environment associated with your vertical (e.g., ``MicroDev04-HP``). This is a one-time set up task. You can reuse the same branch for all subsequent deployments.

	#. Open a terminal, navigate to the ``mdocs`` repo, and enter ``build_mdocs.bat``.
	#. Select option 3 to build ``mDocs`` and ``API`` output.
	#. When complete, commit and push the changes to the ``Mozu.AuthContent repo``. Make sure you push to the correct branch.
	#. Go to `TFS <http://tfs.corp.volusion.com:8080/tfs/VNext/v2Mozu/_build#_a=completed&definitionId=864>`_ and make note of the build name/number. You'll need it for the next step.
	#. Got to `Mozupus <http://mozupus/app#/projects/mozu-authcontent>`_, click the build name/number from the previous step.
	#. Click **Deploy** > **MicroDev04-HP**.
	#. Click **Deploy Now**.

When the build is complete, you can view the docs at one of the following URLs (depending on which environment you deployed to):

	- MicroDev01-HP --> `http://microdev01.dev.volusion.com/docs/index.htm <http://microdev01.dev.volusion.com/docs/index.htm>`_
	- MicroDev02-HP --> `http://microdev02.dev.volusion.com/docs/index.htm <http://microdev02.dev.volusion.com/docs/index.htm>`_
	- MicroDev03-HP --> `http://microdev03.dev.volusion.com/docs/index.htm <http://microdev03.dev.volusion.com/docs/index.htm>`_
	- MicroDev04-HP --> `http://microdev04.dev.volusion.com/docs/index.htm <http://microdev04.dev.volusion.com/docs/index.htm>`_

**Note:** These branches are never merged into ``develop`` or ``master``. The ``develop`` branch gets builds from the ``develop`` branch of the ``mdocs-flare-source`` repo.

****************
Finish a Feature
****************

When you finish a feature, you must enter the following command to merge it back into the develop branch:
	
	``git flow feature finish <my-feature>``

Since everyone on the team could potentially have multiple feature branches that need to be merged for a release, it's best to coordinate when everyone enters the ``feature finish`` command.

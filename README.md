# pyavd-demos

> [!CAUTION]
>  Some of the CloudVision related pyavd functions are still under development and subject to change. These examples were tested with pyavd `5.0.0-devX`.

Run with `uv run pyavd_push_configlet.py --token-file token.tok --apiserver 192.0.2.79`

## Help

```shell
uv run pyavd_push_configlet.py -h
Reading inline script metadata from: pyavd_push_configlet.py
usage: pyavd_push_configlet.py [-h] --token-file token_file --apiserver www.arista.io [--log-level LOGLEVEL] [--dryrun dryrun] [--cc cc]

Pushes Static Configlets to CloudVision using Static Config Studios

options:
  -h, --help            show this help message and exit
  --token-file token_file
                        Location on disk for service account token
  --apiserver www.arista.io
                        endpoint for CVP/CVaaS cluster (must be the www endpoint)
  --log-level LOGLEVEL  Logging level for output. This can be any standard Python logging level (DEBUG, INFO, WARNING, ERROR, CRITICAL). Only the DEBUG and INFO levels are
                        used in this script at present.
  --dryrun dryrun       Creates the workspace and populates inputs, but does not submit workspace when set
  --cc cc               Change control state state: ('pending approval', 'approved', 'running', 'completed', 'deleted', 'failed')

```

## Example run

```shell
 uv run pyavd_push_configlet.py --token-file token.tok --apiserver 192.0.2.79 --cc completed
Reading inline script metadata from: pyavd_push_configlet.py
INFO:root:Script starting
INFO:root:deploy_to_cv:
INFO:root:Creating workspace
INFO:pyavd._cv.workflows.create_workspace_on_cv:create_workspace_on_cv: CVWorkspace(name='AVD 2024-09-23 22:56:48.996564', description=None, id='ws-1a352a32-4c5a-4002-a6aa-c6cbee54cb02', requested_state='submitted', force=False, state=None, change_control_id=None)
INFO:root:Verify devices on CV
INFO:pyavd._cv.workflows.verify_devices_on_cv:verify_devices_on_cv: 6
INFO:pyavd._cv.workflows.verify_devices_on_cv:verify_devices_in_cloudvision_inventory: 0 unique devices.
INFO:pyavd._cv.workflows.verify_devices_on_cv:verify_devices_in_cloudvision_inventory: got 104 matching devices on CV.
INFO:pyavd._cv.workflows.verify_devices_on_cv:verify_devices_in_cloudvision_inventory: 6 existing device objects for 6 unique devices in inventory
INFO:pyavd._cv.workflows.verify_devices_on_cv:verify_devices_in_topology_studio: 6 unique devices for 6 device objects.
INFO:pyavd._cv.workflows.verify_devices_on_cv:verify_devices_in_topology_studio: got 6 devices from I&T Studio.
INFO:root:Deploy configs
INFO:pyavd._cv.workflows.deploy_configs_to_cv:deploy_configs_to_cv: 6
INFO:pyavd._cv.workflows.deploy_configs_to_cv:deploy_configs_to_cv: 0 skipped configs because the devices are missing from CloudVision.
INFO:pyavd._cv.workflows.deploy_configs_to_cv:deploy_configs_to_cv: 6 todo configs.
INFO:pyavd._cv.workflows.deploy_configs_to_cv:deploy_configs_to_cv: Deploying 6 configlets in batches of 20.
INFO:pyavd._cv.workflows.deploy_configs_to_cv:deploy_configs_to_cv: Batch 1
INFO:pyavd._cv.workflows.deploy_configs_to_cv:get_or_create_configlet_root_container: Got AVD root container? True
INFO:pyavd._cv.workflows.deploy_configs_to_cv:deploy_configs_to_cv: 6 existing device containers under AVD root container.
INFO:pyavd._cv.workflows.deploy_configs_to_cv:deploy_configs_to_cv: Deploying 0 configlet assignments / containers in batches of 20.
INFO:root:Deploy studio inputs
INFO:pyavd._cv.workflows.deploy_studio_inputs_to_cv:deploy_studio_inputs_to_cv: 0
INFO:root:Finalizing workspace
INFO:pyavd._cv.workflows.finalize_workspace_on_cv:finalize_workspace_on_cv: CVWorkspace(name='AVD 2024-09-23 22:56:48.996564', description=None, id='ws-1a352a32-4c5a-4002-a6aa-c6cbee54cb02', requested_state='submitted', force=False, state='pending', change_control_id=None)
INFO:pyavd._cv.client.workspace:wait_for_workspace_response: Got response for request 'req-4e6d7673-1919-4c4b-b936-15607a63ab5c': Response(status=ResponseStatus.SUCCESS, message='Build req-4e6d7673-1919-4c4b-b936-15607a63ab5c finished successfully')
INFO:pyavd._cv.workflows.finalize_workspace_on_cv:finalize_workspace_on_cv: CVWorkspace(name='AVD 2024-09-23 22:56:48.996564', description=None, id='ws-1a352a32-4c5a-4002-a6aa-c6cbee54cb02', requested_state='submitted', force=False, state='built', change_control_id=None)
INFO:pyavd._cv.client.workspace:wait_for_workspace_response: Got response for request 'req-c8497010-9c29-4793-b830-9c735ff3d782': Response(status=ResponseStatus.SUCCESS, message='Submitted successfully.')
INFO:pyavd._cv.workflows.finalize_workspace_on_cv:finalize_workspace_on_cv: CVWorkspace(name='AVD 2024-09-23 22:56:48.996564', description=None, id='ws-1a352a32-4c5a-4002-a6aa-c6cbee54cb02', requested_state='submitted', force=False, state='submitted', change_control_id='Workspace-ws-1a352a32-4c5a-4002-a6aa-c6cbee54cb02')
INFO:root:Create/update change control
INFO:pyavd._cv.workflows.finalize_change_control_on_cv:finalize_change_control_on_cv: CVChangeControl(name=None, description=None, id='Workspace-ws-1a352a32-4c5a-4002-a6aa-c6cbee54cb02', change_control_template=None, requested_state='completed', state=None)
INFO:pyavd._cv.workflows.finalize_change_control_on_cv:finalize_change_control_on_cv: CVChangeControl(name='AVD 2024-09-23 22:56:48.996564 (created by workspace)', description='Changes from workspace "AVD 2024-09-23 22:56:48.996564"', id='Workspace-ws-1a352a32-4c5a-4002-a6aa-c6cbee54cb02', change_control_template=None, requested_state='completed', state='approved')
INFO:pyavd._cv.workflows.finalize_change_control_on_cv:finalize_change_control_on_cv: CVChangeControl(name='AVD 2024-09-23 22:56:48.996564 (created by workspace)', description='Changes from workspace "AVD 2024-09-23 22:56:48.996564"', id='Workspace-ws-1a352a32-4c5a-4002-a6aa-c6cbee54cb02', change_control_template=None, requested_state='completed', state='running')
INFO:pyavd._cv.client.change_control:wait_for_change_control_complete: Got response for request 'Workspace-ws-1a352a32-4c5a-4002-a6aa-c6cbee54cb02': COMPLETED
INFO:pyavd._cv.workflows.finalize_change_control_on_cv:finalize_change_control_on_cv: CVChangeControl(name='AVD 2024-09-23 22:56:48.996564 (created by workspace)', description='Changes from workspace "AVD 2024-09-23 22:56:48.996564"', id='Workspace-ws-1a352a32-4c5a-4002-a6aa-c6cbee54cb02', change_control_template=None, requested_state='completed', state='completed')
```

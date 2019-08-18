# Managed Instance Groups and Load Balancing


### Managed Instance Groups

Managed instance gropus are a group of identical VM's that are generated using something called an instance template. This group of VM's can be scaled automatically to meet increasing traffic requirements. For this reason, managed instance groups and load balancing are part of the same solution.

##### Overview

- Pool of similar machines that can be scaled automatically.
- They are created from the same instance template and are identical in every way.
- Typically used with load balancers.
  - Load balancing can be external or internal, global or regional.


### Instance Groups

A group of machines which can be created and managed together to avoid individually controlling each instance in the project.

#### 2 Kinds of Instance Groups

##### Managed

All VM's in this group are identical and have been created from the same image. - Use most of the time.

##### Unmanaged

Group of dis-similar instances. Not created from the same image


## Managed Instance Group

- Supports rolling updates and autoscaling.
- Uses an **instance template** to create a group of **identical** instances.
  - The instance template points to a **public or private** custom image.
- Changes to the instance group changes all instances in the group.
- Can automatically scale the number of instances in the group.
- Work with load balancing to distrubute traffic across instances.
- If an instance stops, crashes or is deleted the group automatically recreates the instance with the same template.
- Can identify and recreate unhealthy instances in a group (autohealing)

### Instance Template

Defines the machine type, image, zone and other properties of an instance. Its a way to save the instance configuration to use it later to create new instances or groups of instances.

- **Global** resource, not bound to zone or region.
- Able to **reference zonal resources** such as persistent disk.
  - In these cases, the template can only be used within that zone.

### Zonal vs Regional MIG

A MIG can be zonal where all the instances are created in the same zone. Or it can be regional where instances are split across the zones in a regin.

- Prefer a regional MIG to zonal so application load can be spread across multiple zones.
  - This protects against failures within a single zone.
- Prefer a zonal MIG if you want lower latency and avoid cross-zone communication.


### Health Checks and Autoscaling

Every MIG has a health check associated with it, it periodically checks the instances to see if they are receiving traffic and if they are healthy.

- A MIG applies health checks to monitor the instances in the group.
- If one or more instances in a group become *unhealthy* (they stop responding to requests). They will be re-created when they are in a MIG. This process is called **autohealing**.
- **Similar to the health checks used in load balancing but the objective is different.**
  - LB health checks are used to determine where to send traffic (which node in the backend pool).
  - MIG health checks are used to recreate instances when they become unhealthy.
- Either of these health checks are not replacements for each other, they should **both be configured**.
- The new instance is re-created based on the template that was **originally used to create** it (might be different from the default instance template)
- When a instance is re-created any disk data may be lost, unless it was explicitly snapshotted.


#### Configuring Health Checks

- **Check Interval:** Time to wait between attempts to check instance health.
- **Timeout:** Length of time to wait for a response before declaring check attempt has failed.
- **Health Threshhold:** How many consecutive *healthy* responses indicate the VM is healthy.
- **Unhealthy Threshold:** How many consecutive *failed* responses indicate VM is unhealthy.


## Unmanaged Instance Groups

- Groups of dissimilar instances that you can add and remove from the group.
  - A group of instances that might be logically grouped together for some reason.
- Do not offer autoscaling, rolling updates or instance templates.
- Not recommended, used only when you need to apply **load balancing to pre-existing configurations**.
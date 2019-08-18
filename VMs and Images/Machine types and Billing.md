# Machine types and Billing

### Cloud Platform Free Tier

Enough for you to keep a very simple website running for free. It includes:

- 1 f1-micro VM instance per month
  - $0.2$VCPU's
  - $0.6$GB
  - Max of 4 persistent disks attached
- 30GB of standard persistent disk storage per month
- 5GB of snapshot stoarge per month
- 1GB of egress from NA to other destinations per month

## Machine Types

### Standard
- 1 vCPU to 3.75GB of RAM ratio

### High Memory

- More memory per vCPU as compared with regular machines.
- Useful for tasks which require more memory as compared to processing.
- $6.5$GB of RAM per core

### High CPU
- More processing power per unit of memory.
- Useful for CPU intensive applications.
- Very little memory for each processor


### Custom Machine
- If none of the predefined machine types fit the workload.
- Save the cost of running on a machine which is more powerful than needed.
- Billed according to the number of **vCPU's and the ammout of memory used.**

## Billing Model

- All machine types are charges for a min on 1 minute
- After the 1st min instances are charged per second

### Shared Core

If you have an application running that does not require a lot of compute, you might use a shared core.
- Ideal for applications that do not require a lot od resources

#### Shared Core Bursting
Shared core machine types dont have much memory or CPU, but they are capable of bursting.
- f1-micro machine types offer **bursting** capabilities that allow instances to use additional physical CPU for short periods of time.
- Bursting happens **automatically** when needed.There is no additional config needed.
- Bursts are not permanent, its only possible **periodically**.
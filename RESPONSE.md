## Part 1

> Terraform and Pulumi both keep a _state file_. Why is state necessary at all — why can't the tool just inspect your AWS account and diff it against your configuration? What does `terraform plan` / `pulumi preview` give you that clicking through the AWS console doesn't?

A state is necessary because the tool would need to associate the resources defined in the code with the actual resources created in AWS. While in code, identifiers given to the desired resources are human-readble, AWS resources may have their their own unique identifiers. So, without a state file, the tool would which AWS resource corresponds with what in the code, so it would not be able to accurately make sure that the application has all the resources it needs to perform correctly, making it difficult ot accurately track and manage the infrastructure. Additionally, the state file stores resource metadata and helps track resources that may have been remoeved from the configurations.

terraform plan or pulumi preview gives the us the ability to review the changes that are about to take places such as showing the downstream resources that are going to be affected by this change, comparing the state file with the live AWS resources for us, and outputting clean text diff that the team can review before committing the change. This helps to reduce undesired changes or break down of other things due to human errors as we can catch these errors in this preview process before deployment.

## Part 2

> Both parts deploy a backend that does the same trivial thing, but they ship it completely differently: Part 1 built a container image, pushed it to a registry, and kept a server running behind a load balancer; Part 2 zipped up one source file and let AWS supply the runtime, with nothing running at all between requests. Compare the two on cold start, cost when idle versus under sustained load, and how each one scales. Part 2 needed far less infrastructure — what did you give up to get that, and when would you still choose Part 1's shape?
> `

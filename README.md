# ECS-Docker-Pipeline

This guide provides step-by-step instructions for setting up a continuous integration and continuous deployment (CI/CD) pipeline for deploying Docker images to Amazon Elastic Container Service (ECS) with EC2 instances using various AWS services.

## Getting Started

These instructions will guide you through the process of creating a fully automated CI/CD pipeline on AWS. The pipeline includes steps for setting up a CodeCommit repository, configuring IAM roles, building Docker images with CodeBuild, storing images in Amazon Elastic Container Registry (ECR), creating ECS infrastructure, and deploying applications with CodePipeline.

### Prerequisites

To follow these steps, you will need:

- An AWS account with appropriate permissions to create and configure resources.
- AWS Command Line Interface (CLI) installed and configured.
- Basic understanding of AWS services such as CodeCommit, CodeBuild, ECR, ECS, and CodePipeline.

## Steps

1. **CodeCommit**: Create a new repository in CodeCommit and obtain the repository's clone URL.

2. **IAM Setup**: Set up a user in IAM with the necessary permissions for ECS, CodeCommit, and CodeBuild. Generate HTTPS Git credentials for the user.

3. **Clone and Push Code to CodeCommit**: Clone the CodeCommit repository to the local machine, add code files, and push changes to CodeCommit.

4. **CodeBuild**: Create a new build project in CodeBuild, configure the source as the CodeCommit repository, and start the build.

5. **ECR (Elastic Container Registry)**: Create a new private repository in ECR to store the Docker images.

6. **BuildSpec File**: Update the BuildSpec file in CodeCommit with the correct Docker image build and push settings.

7. **CodeBuild Service Role**: Create a CodeBuild service role in IAM and attach policies such as "AmazonEC2ContainerRegistryPowerUser" to the role.

8. **Start CodeBuild**: Initiate the CodeBuild project and monitor the build logs to ensure the Docker image is successfully built and pushed to ECR.

9. **ECS Infrastructure**: Use a CloudFormation template to create the ECS infrastructure, including VPC, subnets, and ECS cluster with EC2 instances.

10. **ECS Task Definition**: Create a new ECS task definition with the required container settings and specify the container name and image URI from ECR.

11. **Verify ECS Cluster**: Check the ECS console to confirm the creation of the ECS cluster and monitor container instances to ensure they are running.

12. **CodePipeline Setup**: Set up a CodePipeline in AWS CodePipeline, configure the source (CodeCommit), build (CodeBuild), and deploy (ECS) stages, and add a manual approval step after build for deployment verification.

13. **Code Change and Pipeline Execution**: Make a code change and push it to CodeCommit to observe the pipeline picking up the change, initiating the build, and pausing at the manual approval step. Then manually approve in the AWS CodePipeline console.

14. **Deployment to ECS**: Monitor the deployment status in the AWS CodePipeline console and check the ECS service in the ECS console to verify the deployment status.

15. **Verification of App**: Access the AWS ECS console, find the public IP or DNS of the deployed service, and open the app in a web browser to confirm the code changes.

16. **Cleanup**: After successful verification, delete CodePipeline, CodeBuild project, ECS service, and ECS cluster. Optionally, delete the CodeCommit repository.

## Additional Notes

- If issues occur, adjust the ECS task definition as needed.
- Terminate any running instances and tasks if necessary and recreate them with updated configurations.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)

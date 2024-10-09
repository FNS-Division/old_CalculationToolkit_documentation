# Access Controls and Branching Policies for GitHub Repositories

Remember, the `modified` branch is the one to use for making edits. Administrators will merge changes from `modified` to `main`.

## Repository Structure

### Main Branch (`main`)

- Represents the production-ready code.
- Any changes to this branch will directly update the project in production. There is a pipeline already setup for this branch
- This should be a Protected branch with strict access controls to prevent unauthorized changes.

### Modified Branch (`modified`)

- Serves as the primary development branch where active development occurs.
- All new features, bug fixes, and edits should be based on this branch.
- Acts as an integration point for feature branches before merging into `main`.

## Branching Strategy

To streamline development and maintain code integrity, we adopt a branching strategy inspired by Gitflow, simplified for our project's needs.

### Feature Branches (`feature/your-feature-name`)

- Created from the `modified` branch.
- Used for developing new features, enhancements, or bug fixes.
- **Naming convention:** `feature/brief-description` (e.g., `feature/user-authentication`).

### Hotfix Branches (`hotfix/your-hotfix-name`)

- Created from the `main` branch when critical fixes are needed in production.
- After completion, merged back into both `main` and `modified` branches.

### Release Branches (Optional)

- For preparing a new production release.
- Allows for final testing and minor bug fixes before merging into `main`.

## Access Controls

### Roles and Permissions

#### Owners/Maintainers

- Full access to the repository.
- Can merge pull requests, manage branches, and configure repository settings.
- Responsible for code reviews and approving changes to `main`.

#### Collaborators/Contributors

- Can read and clone the repository.
- Allowed to create branches and submit pull requests.
- Cannot push directly to `main` or `modified` branches.

### Protected Branches

#### `main` Branch

- Protected to prevent direct pushes.
- Requires pull requests for any changes.
- Enforces code review by at least one maintainer before merging.
- Continuous Integration (CI) checks must pass before merging.

#### `modified` Branch

- Also protected to ensure stability.
- Direct pushes are restricted to maintainers.
- Pull requests from feature branches require at least one approval.

## Pull Request Guidelines

To contribute to the project, please follow these steps:

1. **Fork the Repository:**

   - Click the "Fork" button to create your own copy of the repository.
2. **Clone Your Fork:**

   ```bash
   git clone https://ITUINT@dev.azure.com/ITUINT/ConnectivityToolkit/_git/calculation-tools
   ```
3. **Set Upstream Remote (Optional but Recommended):**

   ```bash
   git remote add upstream https://ITUINT@dev.azure.com/ITUINT/ConnectivityToolkit/_git/calculation-tools
   ```
4. **Create a New Feature Branch:**

   ```bash
   git checkout -b feature/your-feature-name modified
   ```
5. **Make Changes and Commit:**

   - Follow the coding standards and guidelines.
   - Write clear and concise commit messages.

   ```bash
   git add .
   git commit -m "Brief description of your changes"
   ```
6. **Push Changes to Your Fork:**

   ```bash
   git push origin feature/your-feature-name
   ```
7. **Submit a Pull Request:**

   - Navigate to the original repository on Azure DevOps.
   - Click on "New Pull Request" and select your feature branch.
   - Ensure the base branch is `modified`.
   - Provide a detailed description of your changes.
8. **Code Review and Approval:**

   - A maintainer will review your pull request.
   - Be responsive to feedback and make necessary changes.
   - Once approved, the pull request will be merged into `modified`.
9. **Merging to `main`:**

   - Periodically, `modified` will be merged into `main` after thorough testing.
   - Only maintainers can perform this action.

## Coding Standards and Guidelines

### Code Quality

- Follow the established coding conventions.
- Write clean, readable, and well-documented code.
- Include comments where necessary.

### Testing

- Write unit tests for new features and bug fixes.
- Ensure all existing tests pass before submitting a pull request.
- Verify that your code does not introduce new bugs.

### Documentation

- Update or create documentation relevant to your changes.
- Ensure installation guides and usage examples are up to date.

## Continuous Integration/Continuous Deployment (CI/CD)

### Automated Checks

- All pull requests will trigger automated tests.
- CI checks must pass before a pull request can be merged.
- Tests include code linting, unit tests, and build verification.

### Deployment

- Changes merged into `main` will automatically deploy to production.
- Ensure that all changes to `main` are stable and production-ready.

## Issue Tracking and Management

### Reporting Issues

- Use the **Issues** tab to report bugs or request features.
- Provide a clear and detailed description.

### Assigning and Labeling

- Maintainers will triage issues and assign labels.
- Contributors can comment on issues they'd like to address.

## Community Guidelines

### Code of Conduct

- Be respectful and inclusive.
- Constructive feedback is encouraged.
- Harassment or discrimination will not be tolerated.

### Communication

- Use clear and professional language.
- Keep discussions relevant to the project.

## Security Practices

### Sensitive Information

- Do not commit secrets, passwords, or API keys to the repository.
- Use environment variables or secure vaults for sensitive data.

### Vulnerability Reporting

- If you discover a security vulnerability, report it privately to the maintainers.
- Do not create a public issue for security concerns.

## Access Request Procedure

### Becoming a Collaborator

- Regular contributors may be invited to become collaborators.
- Demonstrate consistent, quality contributions to be considered.

### Maintainer Role

- Maintainers are appointed based on significant contributions and commitment.
- Responsible for guiding the project's direction.

## Branch Deletion Policy

### Feature Branches

- After a feature branch has been merged, it should be deleted to keep the repository clean.
- This can be done by maintainers or the contributor who submitted the pull request.

## Release Management

### Versioning

- Use semantic versioning for releases (e.g., `v1.2.3`).
- Tags should be created for each release.

### Changelog

- Maintain a changelog documenting new features, fixes, and breaking changes.

## Backup and Recovery

### Repository Backup

- Regular backups of the repository should be maintained.
- Use Azure DevOps' archival features or external backup solutions.

### Disaster Recovery

- In case of data loss, backups can be restored by maintainers.

## Compliance and Legal

### Licensing

- Clearly state the open-source license (e.g., MIT, Apache 2.0) in the repository.
- Ensure all contributions comply with the license terms.

### Contributor License Agreement (CLA)

- Contributors may be required to sign a CLA.
- This ensures that contributions are licensed appropriately.

## Additional Notes

### Continuous Improvement

- This policy is subject to change.
- Suggestions for improvements are welcome via pull requests or issues.

### Acknowledgments

- Contributors will be acknowledged in the project's documentation.

---

**Repository Link:** [calculation-tools](https://ITUINT@dev.azure.com/ITUINT/ConnectivityToolkit/_git/calculation-tools)

_Remember, the `modified` branch is the one to use for making edits. Administrators will merge changes from `modified` to `main`._

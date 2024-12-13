Sure! If you'd like to remove the CI/CD option and keep the process manual for now, here's a simplified version of the workflow using only `main` and `stable` branches without automation:

### **Final Git Branching Strategy**

1. **`main` (Production Inversion)**:
   - **`main` will always contain production-ready, stable code**. It is **untouched** and will only be updated with code that has been fully validated and tested.
   - **No feature work or testing happens directly on `main`**. Only verified, stable releases get merged into `main`.
   - **`main` is what is used for production deployments**. Code in `main` is trusted to be stable and ready to go live.

2. **`stable` (Development, Testing, and Release Preparation)**:
   - **`stable` is where all development, testing, and release preparation happen**.
   - **Features**: New features, bug fixes, and development work will happen here. Engineers can safely work on new code and test it.
   - **Testing**: All testing (unit tests, integration tests, manual testing, etc.) will happen on the `stable` branch. Once the code is verified as working and stable, it will be prepared for release.
   - **Release Tagging**: Releases will be tagged on the `stable` branch, and the code will be tested before merging it into `main`.

3. **Feature Development**:
   - Developers will create **feature branches from `stable`** to work on individual features or fixes:
     ```bash
     git checkout stable
     git checkout -b feature/login
     ```
   - After completing a feature and testing it, it will be merged into `stable`:
     ```bash
     git checkout stable
     git merge feature/login
     git push origin stable
     ```

4. **Tagging and Release Preparation**:
   - Once all features are integrated and tested on `stable`, and the code is verified to be stable, it is time to create a **tag for the release**:
     ```bash
     git checkout stable
     git pull origin stable
     git tag -a v1.0.0 -m "Release version 1.0.0"
     git push origin v1.0.0
     ```
   - After tagging, you can manually deploy the release from `stable` to a staging or testing environment for final verification.

5. **Merging `stable` into `main`**:
   - After the release is validated in the staging or testing environment, **merge `stable` into `main`**:
     ```bash
     git checkout main
     git pull origin main
     git merge stable
     git push origin main
     ```

6. **Deploying from `main`**:
   - Finally, the code in `main`, which contains the stable, verified release, is deployed to **production**.
   - Deployment can be done manually (for example, using scripts, manually uploading code, etc.).

### **Step-by-Step Example**

1. **Feature Development**:
   - A developer starts working on a new feature (e.g., user login) by creating a feature branch from `stable`:
     ```bash
     git checkout stable
     git checkout -b feature/login
     ```
   - The feature is developed, and the developer commits the changes:
     ```bash
     git add .
     git commit -m "Added user login feature"
     git push origin feature/login
     ```

2. **Merging Feature into `stable`**:
   - After the feature is complete and tested, it is merged back into `stable`:
     ```bash
     git checkout stable
     git merge feature/login
     git push origin stable
     ```

3. **Testing and Validation on `stable`**:
   - The code is manually tested on `stable` (either through manual verification or local testing). You can also deploy to a **staging environment** to do more thorough validation.

4. **Tagging the Release**:
   - After everything is tested and ready for production, create a **tag for the release** on `stable`:
     ```bash
     git checkout stable
     git pull origin stable
     git tag -a v1.0.0 -m "Release version 1.0.0"
     git push origin v1.0.0
     ```

5. **Merging into `main`**:
   - After the release is tagged and validated, **merge the changes from `stable` into `main`** to update the production code:
     ```bash
     git checkout main
     git pull origin main
     git merge stable
     git push origin main
     ```

6. **Deploying from `main`**:
   - Finally, the **release version** is deployed from `main` to production.

### **Summary:**
- **`main`**: Contains production-ready code and will only be updated after thorough testing.
- **`stable`**: Used for all development, feature testing, and preparing releases. This is where features are merged, tagged, and verified.
- **Feature branches**: Developers work in feature branches created from `stable`.
- **Release tagging**: After testing, a release tag is created on `stable`, and once it's verified, it gets merged into `main` for deployment.

This setup ensures that `main` remains untouched and always reflects the **stable, production-ready code**, while `stable` becomes the **branch for testing, feature integration, and preparing releases**.
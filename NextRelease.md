To prepare for your next release and tag, here’s a straightforward manual process you can follow using the `main` and `stable` branches.

### **Steps for Preparing and Tagging the Next Release**

#### **1. Ensure `stable` is up to date**
   - Make sure that the `stable` branch has the latest changes, and it's fully tested and validated.
   - **If you're not already on `stable`**, switch to it and pull the latest changes from the remote repository:
     ```bash
     git checkout stable
     git pull origin stable
     ```

#### **2. Merging New Changes into `stable`**
   - If there are any recent changes on `main` (like bug fixes or new features), you may need to merge `main` into `stable` before tagging the release.
   - **Merge `main` into `stable`**:
     ```bash
     git checkout stable
     git pull origin stable  # Ensure you're up-to-date
     git merge main  # Merge any changes from `main` into `stable`
     git push origin stable
     ```
   - After merging, make sure everything is tested in `stable`.

#### **3. Create a Tag for the Next Release**
   - Once `stable` is ready for the next release, you will create a tag.
   - **Tagging the Release**: Use a semantic versioning format (`vX.X.X`) for versioning your releases. The first number indicates major changes, the second is for backward-compatible feature changes, and the third for patches.
     - For example, if the previous version was `v1.0.0`, and you're making the first release after that, you would use `v1.1.0` or `v1.0.1` for a minor or patch update respectively.
     ```bash
     git checkout stable  # Ensure you're on stable
     git pull origin stable  # Get the latest changes
     git tag -a v1.1.0 -m "Release version 1.1.0"  # Create a new tag
     git push origin v1.1.0  # Push the tag to remote
     ```

#### **4. Merge `stable` into `main` (Optional)**
   - Once you’ve tagged the release in `stable`, you can merge the changes from `stable` into `main`. This will update the `main` branch with the latest production-ready code and mark the new release version for deployment.
     ```bash
     git checkout main
     git pull origin main  # Ensure you're up-to-date
     git merge stable  # Merge the changes from stable
     git push origin main  # Push the changes to remote
     ```

#### **5. Deploy the Release**
   - Now that `main` is up to date with the latest version, you can deploy the code from `main` to your production environment.

### **Summary of Steps for Tagging the Next Release**
1. Ensure `stable` has all the latest code and changes, and test it.
2. If needed, merge `main` into `stable` to bring in any important changes.
3. Create a tag on `stable` (e.g., `v1.1.0`) to mark the next release.
4. Optionally, merge `stable` into `main` for deployment.
5. Deploy from `main` to production.

This ensures that you have a clean and controlled process for creating releases, tagging versions, and ensuring that your `main` branch always reflects stable, production-ready code.
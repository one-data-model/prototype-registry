# prototype-registry

Submitter  |    Administrator   | OneDM Working Group  |    Description
-----------|--------------------|----------------------|---------------------
  **1**    | .                  |  .                   |  **Submitter** raises an [Issue](https://github.com/one-data-model/prototype-registry/issues)
   .       | **2**              |  .                   |  **Administrator** reviews **Submitter's Issue** and decides if the **Issue** is rejected or it is moved to the next step.
   .       | **3**              |  -                   |  **Administrator** creates a **feature-branch** based on **Submitter's Issue** information.
  **4**    | .                  | .                    |  **Submitter** sends a Pull Request (PR) against the **feature-branch** created by the Administrator.
  .        | **5**              | .                    |  **Administrator** validates the **Submitter's PR** and provides advice accordingly.
  .        | **6**              | .                    |  **Submitter**  updates the PR based on **Administrator** feedback or Working Group discussion (step 7).
  .        | .                  | **7**                |  **Submitter** and Working Group discuss **Submitter's PR**
  .        | .                  | **8**                |  **Working Group** decides if the PR is accepted (merged) or rejected (closed).
  .        | .                  | **9**                |  **Working Group Chair** merges **Submitter's PR** into **feature-branch**.
  .        | **10**             | .                    |  **Administrator** perform a final validation and check before merging into **verification** branch.
  .        | **11**             | .                    |  **Workig Group** request the **Administrator** to create a new release by merging the **verification** branch into the **master** branch.

  
  
![image](https://user-images.githubusercontent.com/3258579/67356812-69f0f300-f553-11e9-8056-5eb410a9215c.png)

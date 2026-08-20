# Ex.No 05 – Simulate a Cloud Scenario Using CloudSim

## Aim
To simulate a cloud scenario using CloudSim and run a scheduling algorithm that is not present in CloudSim.

## Tools Used
- Eclipse IDE for Java Developers
- CloudSim 3.0.3
- Apache Commons Math 3.6.1

## Procedure

1. **Download Eclipse** (Windows x86_64) from:
   https://www.eclipse.org/downloads/packages/release/kepler/sr1/eclipse-ide-java-developers

2. **Download CloudSim 3.0.3** from GitHub:
   https://github.com/Cloudslab/cloudsim/releases/tag/cloudsim-3.0.3

3. **Download Apache Commons Math 3.6.1**:
   https://commons.apache.org/proper/commons-math/download_math.cgi
   (`commons-math3-3.6.1-bin.zip`)

4. Extract `cloudsim-3.0.3` and `commons-math3-3.6.1` on your local machine.

5. Open `Eclipse.exe`.

6. **File → New → Project…** to open the New Project wizard.

7. Select **Java Project** and click **Next**.

8. Set **Project name**: `Cloudsim`.

9. Uncheck **Use default location**, click **Browse**, and select the folder where you unzipped CloudSim (should contain `bin`, `docs`, `examples`, etc.), then click **Next**.

10. Verify the source path is set correctly, then click **Next** to configure project settings.

11. In the **Libraries** tab, check whether `commons-math3-3.x.jar` is present. If not, click **Add External JARs…**

12. Browse to the extracted Commons Math folder, select `commons-math3-3.x.jar`, and click **Open**.

13. Confirm the JAR appears in the library list, then click **Finish**. (Eclipse may take a few minutes to configure the project.)

14. In **Project Explorer**, navigate to `examples` → `org.cloudbus.cloudsim.examples` and double-click `CloudSimExample1.java` to open it.

15. Run the example: **Run → Run** (or `Ctrl + F11`).

16. On successful execution, the Eclipse console displays output such as:
    ```
    Starting CloudSimExample1...
    Initialising...
    Starting CloudSim version 3.0
    Datacenter_0 is starting...
    Broker is starting...
    ...
    ========== OUTPUT ==========
    Cloudlet ID    STATUS    Data center ID    VM ID    Time    Start Time    Finish Time
    0              SUCCESS   2                 0        400     0.1           400.1
    CloudSimExample1 finished!
    ```

## Notes
To fulfill the "scheduling algorithm not present in CloudSim" part of the aim, extend/override the VM scheduler (e.g., `VmScheduler`, `CloudletScheduler`) with a custom algorithm (e.g., Round Robin, Priority-based, or a custom heuristic) and reference it in your Datacenter/Broker setup.

## Result
CloudSim was successfully simulated in the Eclipse environment.

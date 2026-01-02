# Meter Data Retrieval

# Overview
SEL-735 meters store historical data in a load data profile (LDP) recorder. Use this procedure to retrieve this data from a meter.
# Prerequisites
*   A connection to a meter with engineering access. This can be accomplished via:
    *   A direct IP connection to a meter's interface that has Telnet enabled
    *   A direct serial connection
    *   A connection tunneled through an RTAC, provided that a direct transparent connection method is used
*   AcSELerator QuickSet (SEL-5030) software
# Method
1. Open AcSELerator QuickSet. From the menu bar, select **Communications** > **Parameters**.
2. Enter the communications parameters for the connection.
    *   **Serial Connection**
        *   For **Active Connection Type**, select **Serial**. The **Serial** tab will become active.
        *   From the **Device** dropdown, select the COM port that is connected to the meter.
        *   Select the **Data Speed**, **Data Bits**, **Stop Bits**, **Parity**, **RTS/CTS**, **DTR**, **XON/XOFF**, and **RTS** settings to match what is configured on the meter's serial interface.
            *   If RTS/CTS is not used on the meter, set **XON/XOFF** to **On**.
            *   If RTS/CTS is used on the meter, set **XON/XOFF** to **Off**.
            *   **DTR** is **On** by default.
        *   Enter the **Level One Password** (required) and **Level Two Password** (optional) if they are different from the defaults.
        *   Select **OK** to connect.
    *   **Network Connection**
        *   For **Active Connection Type**, select **Network**. The **Network** tab will become active.
        *   Enter the meter's IP address in the **Host IP Address** field.
        *   Enter `23` for **Port Number**.
        *   For **File Transfer Option**, select **Telnet**.
        *   Enter the **Level One Password** (required) and **Level Two Password** (optional) if they are different from the defaults.
        *   Select **OK** to connect.
    *   **RTAC Engineering Access Connection**
        *   For **Active Connection Type**, select **Network**. The **Network** tab will become active.
        *   Enter the RTAC's IP address in the **Host IP Address** field.
        *   For **Port Number**, enter the port number that was entered in the **Server IP Port** setting in the RTAC's SEL Server device. The standard for CEG projects is 50000.
        *   For **File Transfer Option**, select the option that was selected in the **Serial Tunneling Mode** setting in the RTAC's SEL Server device. The standard for CEG projects is SSH.
        *   Enter your RTAC credentials in **User ID** and **Password**.
        *   Enter the **Level One Password** (required) and **Level Two Password** (optional) if they are different from the defaults.
        *   Select **OK** to connect.
        *   If SSH was selected, a warning may appear, asking if you trust the connection. Confirm your trust and allow the connection.
        *   Open the Terminal.
            1. Type `ACC <Enter>` to log in to Level 1.
            2. Type `WHO <Enter>` to view a list of devices and their virtual port numbers.
            3. Type `POR N D <Enter>` where `N` is the virtual port number of the meter. The `D` tells the RTAC that you wish to have a direct transparent connection. The HMI does not work without a direct transparent connection.
            4. You will now be connected to the meter. Press `<Enter>` a few times to see that the meter's `=` prompt appears. Type `QUI <Enter>` to see a banner that identifies the meter, so that you can verify that you are connected to the correct device.
            5. Type `ACC <Enter>` to log in to Level 1 of the meter. You will see a `=>` prompt to indicate that you are at Level 1.
3. Open the HMI either by selecting the meter icon on the toolbar or by selecting **Tools** > **HMI** > **HMI**. The HMI will take a moment to load.
4. After the HMI loads, select **LDP Data Viewer**. Navigate to the **Export** tab.
5. From **Export Format**, select **CSV**.
6. Select the recorder(s) you wish to download.
7. Set **Scale**, **Unit Scale**, and **Date Range** to your desired values. Usually you will want to choose **Primary** for **Scale**. Set **Date Range** to **Custom** to pick a custom date range.
8. Select **Export** to save the data. You will be asked for a location to save the files.
9. When complete, you may close the HMI window. Disconnect communications by selecting **Communications** > **Disconnect**.

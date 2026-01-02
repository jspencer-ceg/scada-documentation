#####################
RTAC POU pin settings
#####################

Configure POU pin settings to collect SER data from a device.

.. note::
   The method for enabling SER data collection changed beginning with RTAC firmware versions R155 and R201. These steps only apply to R200, R154, and below.

.. note::
   The SEL-587 does not support SOE collection. Skip these steps for that relay.

1. Select the SEL client device that you are using for SER data and event collection from the :guilabel:`Project` pane and go to the :guilabel:`POU Pin Settings` tab.

#. To enable SER data collection, set :guilabel:`Enable_ASCII_SER_Logging` to :guilabel:`True` in the :guilabel:`Default Value` column.

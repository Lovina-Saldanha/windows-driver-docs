---
title: Bluetooth Appendix
description: Contains Microsoft-defined Bluetooth HCI extension examples and diagrams.
ms.assetid: 5C3C2479-03F9-4D33-94DA-3371D84C514B
ms.date: 04/20/2017
ms.localizationpriority: medium
---

# Bluetooth Appendix

This section contains Microsoft-defined Bluetooth HCI extension examples and diagrams.

## Example: Matching patterns for HCI_VS_MSFT_LE_Monitor_Advertisement

This example shows a received HCI_VS_MSFT_LE_Monitor_Advertisement command and the evaluations of 3 different advertisement packets against the command parameters.

Received HCI_VS_MSFT_LE_Monitor_Advertisement command
An HCI_VS_MSFT_LE_Monitor_Advertisement command is received by the controller and contains the following parameters.

<table>
<tr>
<th>Parameter</th>
<th>Value</th>
<th></th>
</tr>
<tr>
<td>
<p><i>Subcommand_opcode</i></p>
</td>
<td>
<p>0x03</p>
</td>
<td>
<p>Subcommand opcode for HCI_VS_MSFT_LE_Monitor_Advertisement</p>
</td>
</tr>
<tr>
<td>
<p><i>RSSI_threshold_high</i></p>
</td>
<td>
<p>0x01</p>
</td>
<td>
<p>1dB</p>
</td>
</tr>
<tr>
<td>
<p><i>RSSI_threshold_low</i></p>
</td>
<td>
<p>0xCE</p>
</td>
<td>
<p>-50dB</p>
</td>
</tr>
<tr>
<td>
<p><i>RSSI_threshold_low_time_interval</i></p>
</td>
<td>
<p>0x05</p>
</td>
<td>
<p>5 seconds</p>
</td>
</tr>
<tr>
<td>
<p><i>RSSI_sampling_period</i></p>
</td>
<td>
<p>0xFF</p>
</td>
<td>
<p>No sampling</p>
</td>
</tr>
<tr>
<td>
<p><i>Condition_type</i></p>
</td>
<td>
<p>0x01</p>
</td>
<td>
<p><i>Condition</i> is a pattern</p>
</td>
</tr>
<tr>
<td rowspan="12">
<p><i>Condition</i></p>
</td>
<td>
<p>0x02</p>
</td>
<td>
<p>2 patterns should be matched</p>
</td>
</tr>
<tr>
<td>
<p>0x03</p>
</td>
<td>
<p>Length of first pattern, including AD Type and starting position</p>
</td>
</tr>
<tr>
<td>
<p>0x01</p>
</td>
<td>
<p>AD Type</p>
</td>
</tr>
<tr>
<td>
<p>0x00</p>
</td>
<td>
<p>Starting position following the AD Type</p>
</td>
</tr>
<tr>
<td>
<p>0x01</p>
</td>
<td>
<p>First pattern to be matched</p>
</td>
</tr>
<tr>
<td>
<p>0x06</p>
</td>
<td>
<p>Length of second pattern, including AD Type and starting position</p>
</td>
</tr>
<tr>
<td>
<p>0xFF</p>
</td>
<td>
<p>AD Type (Manufacturer specific data)</p>
</td>
</tr>
<tr>
<td>
<p>0x00</p>
</td>
<td>
<p>Starting position following the AD Type</p>
</td>
</tr>
<tr>
<td>
<p>0x00</p>
</td>
<td rowspan="4">
<p>Second pattern to be matched</p>
</td>
</tr>
<tr>
<td>
<p>0x06</p>
</td>
</tr>
<tr>
<td>
<p>0xFF</p>
</td>
</tr>
<tr>
<td>
<p>0xFF</p>
</td>
</tr>
</table>
<p> </p>
The controller then receives the following advertisement packets.


-    Advertisement packet [A] 
0x02 0x01 0x01 0x07 0x09 0x54 0x61 0x62 0x6C 0x65 0x74 0x05 0xFF 0x00 0x06 0xFF 0xFF

-    Advertisement packet [B] 
0x02 0x01 0x01 0x07 0x09 0x54 0x61 0x62 0x6C 0x65 0x74 0x05 0xFF 0x00 0x06 0xFF 0x01

-    Advertisement packet [C] 
0x07 0x09 0x54 0x61 0x62 0x6C 0x65 0x74 0x05 0xFF 0x00 0x06 0xFF 0xFF

</dd>
</dl>

### Evaluating match for Advertisement packet [A]

<table>
<tr>
<td>
<p>AD Type of first pattern to be matched</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>Length of first pattern to be matched</p>
</td>
<td>
<p>0x03 - 0x02 = 0x01 byte</p>
</td>
</tr>
<tr>
<td>
<p>Pattern to be matched at position 0x00 for AD Type 0x01</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>Bytes at position 0x00 for the AD Type 0x01</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>AD Type of second pattern to be matched</p>
</td>
<td>
<p>0xFF (Manufacturer specific data)</p>
</td>
</tr>
<tr>
<td>
<p>Length of second patter to be matched</p>
</td>
<td>
<p>0x06 - 0x02 = 0x04 bytes</p>
</td>
</tr>
<tr>
<td>
<p>Pattern to be matched at position 0x00 for AD Type 0xFF</p>
</td>
<td>
<p>0x00 0x06 0xFF 0xFF</p>
</td>
</tr>
<tr>
<td>
<p>Bytes at position 0x00 for the AD Type 0xFF</p>
</td>
<td>
<p>0x00 0x06 0xFF 0xFF</p>
</td>
</tr>
<tr>
<td colspan="2">
<p><b>Verdict: PASS</b></p>
</td>
</tr>
</table>
  


### Evaluating match for Advertisement packet [B]
<table>
<tr>
<td>
<p>AD Type of first pattern to be matched</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>Length of first pattern to be matched</p>
</td>
<td>
<p>0x03 - 0x02 = 0x01 byte</p>
</td>
</tr>
<tr>
<td>
<p>Pattern to be matched at position 0x00 for AD Type 0x01</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>Bytes at position 0x00 for the AD Type 0x01</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>AD Type of second pattern to be matched</p>
</td>
<td>
<p>0xFF (Manufacturer specific data)</p>
</td>
</tr>
<tr>
<td>
<p>Length of second patter to be matched</p>
</td>
<td>
<p>0x06 - 0x02 = 0x04 bytes</p>
</td>
</tr>
<tr>
<td>
<p>Pattern to be matched at position 0x00 for AD Type 0xFF</p>
</td>
<td>
<p>0x00 0x06 0xFF <b>0xFF</b></p>
</td>
</tr>
<tr>
<td>
<p>Bytes at position 0x00 for the AD Type 0xFF</p>
</td>
<td>
<p>0x00 0x06 0xFF <b>0x01</b></p>
</td>
</tr>
<tr>
<td colspan="2">
<p><b>Verdict: PASS</b></p>
</td>
</tr>
</table>
 
### Evaluating match for Advertisement packet [C]
<table>
<tr>
<td>
<p>AD Type of first pattern to be matched</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>Length of first pattern to be matched</p>
</td>
<td>
<p>0x03 - 0x02 = 0x01 byte</p>
</td>
</tr>
<tr>
<td>
<p>Pattern to be matched at position 0x00 for AD Type 0x01</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>Bytes at position 0x00 for the AD Type 0x01</p>
</td>
<td>
<p>Undefined. The advertisement does not have data with AD Type 0x01.</p>
</td>
</tr>
<tr>
<td colspan="2">
<p><b>Verdict: FAIL</b></p>
</td>
</tr>
</table>

## Example: Advertisement monitoring

This example illustrates RSSI advertisement monitoring. The RSSI values for received advertisements that matched a specified condition are shown below.

<table>
<tr>
<th>Time (s)</th>
<th>RSSI (dB)</th>
</tr>
<tr>
<td>1</td>
<td>-100</td>
</tr>
<tr>
<td>2</td>
<td>-90</td>
</tr>
<tr>
<td>3</td>
<td>-5</td>
</tr>
<tr>
<td>4</td>
<td>-15</td>
</tr>
<tr>
<td>5</td>
<td>-30</td>
</tr>
<tr>
<td>6</td>
<td>-15</td>
</tr>
<tr>
<td>7</td>
<td>-45</td>
</tr>
<tr>
<td>8</td>
<td>-20</td>
</tr>
<tr>
<td>9</td>
<td>-35</td>
</tr>
<tr>
<td>10</td>
<td>-45</td>
</tr>
<tr>
<td>11</td>
<td>-70</td>
</tr>
<tr>
<td>12</td>
<td>-85</td>
</tr>
<tr>
<td>13</td>
<td>-85</td>
</tr>
<tr>
<td>14</td>
<td>-85</td>
</tr>
<tr>
<td>15</td>
<td>-90</td>
</tr>
<tr>
<td>16</td>
<td>-90</td>
</tr>
<tr>
<td>17</td>
<td>-70</td>
</tr>
</table>
<p> </p>
<table>


<table>
<tr>
<th>Parameter</th>
<th>Value</th>
</tr>
<tr>
<td><i>RSSI_threshold_high</i></td>
<td>-10dB</td>
</tr>
<tr>
<td><i>RSSI_threshold_low</i></td>
<td>-80dB</td>
</tr>
<tr>
<td><i>RSSI_threshold_low_time_interval</i></td>
<td>3 seconds</td>
</tr>
<tr>
<td><i>RSSI_sampling_period</i></td>
<td>2 seconds</td>
</tr>
</table>

</p><img src="images/HCI_Example_Advertisement_Monitoring.png" alt="Advertisement monitoring graph"/><p>

The advertisement RSSI is greater than RSSI_threshold_high at time 3. The periodic timer for sampling starts at time 3. Every 2 seconds, the periodic timer expires and the average RSSI value of the received advertisement is propagated to the stack.

When the periodic timer expires at time 5, the average of the advertisement RSSIs received during this time (-23dB) is propagated to the stack.

When the periodic timer expires at time 13, the average of the advertisement RSSIs received during this timeframe is below RSSI_threshold_low (-80dB). The average of the advertisement RSSI (-85 dB) should be propagated to the host.

When RSSI_threshold_low_time_interval expires at instant 15, an advertisement is propagated to the host with RSSI of -85dB. No further advertisements are sent to the host in this example.

 ## Flowchart: Advertisement and allow list filtering

This flowchart provides an example controller implementation of advertisement filtering and allow list filtering when an advertisement is received.

A controller can implement this logic differently, as long as the host is notified of the advertisement or <MSHelp:link tabindex="0" keywords="bltooth.hci_vs_msft_le_monitor_device_event"><b>HCI_VS_MSFT_LE_Monitor_Device_Event</b></MSHelp:link> as specified by the flowchart.

<p><img src="images/HCI_Filtering_Flowchart.png" alt="Microsoft HCI extension filtering flowchart"/></p>

## Sequence diagram: Propagate scan response associated with advertisement

Sequence diagram: Propagate scan response associated with advertisement

This sequence diagram shows a propagate scan response that is associated with an advertisement that satisfies an advertisement filter when active scanning is enabled.
This diagram only shows the expected sequence of events between controller and host, and does not show events between the controller and a particular device.
Assume that there is an advertisement <i>A</i> that satisfies an advertisement filter, and an advertisement <i>B</i> that does not satisfy the advertisement filter.
<p> <img src="images/HCI_Propagate_Scan_Sequence.png" alt="HCI propagate scan sequence diagram"/></p>

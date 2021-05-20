![](RackMultipart20210520-4-cjssah_html_6e4eda26a3e5fd14.png)

# External PHY Recovered Clock

# Proposal

| **Title** | **External PHY Abstraction Interface** |
| --- | --- |
| **Authors** | **Broadcom** |
| **Status** | **Draft** |
| **Type** |
 |
| **Created** | **05/20/2021** |
| **SAI-Version** | **0.1** |

# **Contents**

[List of Changes](#_Toc68201129)

[1 Overview](#_Toc68201130)

[1.1 Recovered Clock (SyncE) Configuration on PHY ](#_Toc68201131)

[2 Configuration Example ](#_Toc68201132)

# List of Changes

| **Version** | **Changes** | **Name** | **Date** |
| --- | --- | --- | --- |
| 0.1 | Proposal for PAI Recovered Clock | | 04/01/2021 |


# Overview

The purpose of this document is to describe Recovered Clock (SyncE) functionality and interface to manage Recovered Clock functionality of the PHY. PHY is the connector between MAC (SerDes) and physical medium such as optical fiber or copper transceivers. Recovered Clock derived from the line, locked to the incoming data rate. SyncE, short for Synchronous Ethernet, is a method to transfer frequency over the Ethernet physical layer across a network traceable to a reference clock.


## Recovered Clock (SyncE) Configuration on PHY

Recovered Clock (SyncE) can be configured on the PHY.

# Additions to saiport.h
/**
 * @brief Attribute data for #SAI_PORT_ATTR_SYNCE_GEN_SQUELCH_CONFIG
 * Used for Recovered Clock Generation and Squelch Mode Configuration
 */

typedef enum _sai_port_synce_gen_squelch_config_t
{

    /** Disable clock Gen and Squelch */
    SAI_PORT_SYNCE_GEN_SQUELCH_CONFIG_DISABLE,

    /** Enable clock Gen only, no squelch needed (Clock is always sent out) */
    SAI_PORT_SYNCE_GEN_SQUELCH_CONFIG_NONE,

    /** Squelch clock on Loss of Signal (LOS) */
    SAI_PORT_SYNCE_GEN_SQUELCH_CONFIG_LOS,

    /** Squelch clock on Loss of Lock (LOL) */
    SAI_PORT_SYNCE_GEN_SQUELCH_CONFIG_LOL,

    /** Squelch clock on Loss of Signal(LOS) or Loss of Lock(LOL) */
    SAI_PORT_SYNCE_GEN_SQUELCH_CONFIG_LOS_OR_LOL,

    /** Force Squelch */
    SAI_PORT_SYNCE_GEN_SQUELCH_CONFIG_FORCE
} sai_port_synce_gen_squelch_config_t;
 

/**
 * @brief Attribute data for #SAI_PORT_ATTR_SYNCE_DIVIDER
 * Divider selection to apply on Line/Lane rate before outputting clock
 */
 
typedef enum _sai_port_synce_divider_t
{

    /** Divide by 20 */
    SAI_PORT_SYNCE_DIVIDER_20,

    /** Divide by 40 */
    SAI_PORT_SYNCE_DIVIDER_40,

    /** Divide by 80 */
    SAI_PORT_SYNCE_DIVIDER_80,

    /** Divide by 160 */
    SAI_PORT_SYNCE_DIVIDER_160,

    /** Divide by 400 */
    SAI_PORT_SYNCE_DIVIDER_400,

    /** Divide by 1000 */
    SAI_PORT_SYNCE_DIVIDER_1000,

    /** Divide by 64 */
    SAI_PORT_SYNCE_DIVIDER_64,

    /** Divide by 128 */
    SAI_PORT_SYNCE_DIVIDER_128,

    /** Divide by 256 */
    SAI_PORT_SYNCE_DIVIDER_256,

    /** Divide by 512 */
    SAI_PORT_SYNCE_DIVIDER_512,

    /** Divide by 1024 */
    SAI_PORT_SYNCE_DIVIDER_1024,

    /** Divide by 2048 */
    SAI_PORT_SYNCE_DIVIDER_2048,

    /** Divide by 4096 */
    SAI_PORT_SYNCE_DIVIDER_4096,

    /** Divide by 8192 */
    SAI_PORT_SYNCE_DIVIDER_8192,

    /** Divide by 32 */
    SAI_PORT_SYNCE_DIVIDER_32,

    /** Divide by 120 */
    SAI_PORT_SYNCE_DIVIDER_120,

    /** Divide by 240 */
    SAI_PORT_SYNCE_DIVIDER_240,

    /** Divide by 520 */
    SAI_PORT_SYNCE_DIVIDER_520,

    /** Divide by 2040 */
    SAI_PORT_SYNCE_DIVIDER_2040,

    /** Divide by 4080 */
    SAI_PORT_SYNCE_DIVIDER_4080,

    /** Divide by 1. */
    SAI_PORT_SYNCE_DIVIDER_1,

    /** Divide by 2. */
    SAI_PORT_SYNCE_DIVIDER_2,

    /** Divide by 4. */
    SAI_PORT_SYNCE_DIVIDER_4,

    /** Divide by 8. */
    SAI_PORT_SYNCE_DIVIDER_8,

    /** Divide by 16. */
    SAI_PORT_SYNCE_DIVIDER_16,

    /** Divide by 66. */
    SAI_PORT_SYNCE_DIVIDER_66,

    /** Divide by 82.5. */
    SAI_PORT_SYNCE_DIVIDER_82P5,

    /** Divide by 528. */
    SAI_PORT_SYNCE_DIVIDER_528
} sai_port_synce_divider_t;    


    /**
     * @brief Recovered Clock Generation enable/disable and Squelch Mode Configuration
     *
     * @type sai_port_synce_gen_squelch_config_t
     * @flags CREATE_AND_SET
     * @default SAI_PORT_SYNCE_GEN_SQUELCH_CONFIG_DISABLE
     */
    SAI_PORT_ATTR_SYNCE_GEN_SQUELCH_CONFIG,

    /**
     * @brief Recovered Clock Lane selection from global lane of phy_id
     *
     * @type sai_uint32_t
     * @flags CREATE_AND_SET
     * @default 0
     */
    SAI_PORT_ATTR_SYNCE_CLOCK_OUTPUT_LANE,

    /**
     * @brief Package Lanes that need to be monitored for Loss of Signal or Loss of Line
     *
     * @type sai_uint32_t
     * @flags CREATE_AND_SET
     * @default 0
     */
    SAI_PORT_ATTR_SYNCE_SQUELCH_MONITOR_LANES,

    /**
     * @brief Divider selection to apply on Line/Lane rate before outputting clock
     *
     * @type sai_port_synce_divider_t
     * @flags CREATE_AND_SET
     * @default SAI_PORT_SYNCE_DIVIDER_20
     */
    SAI_PORT_ATTR_SYNCE_DIVIDER,

    /**
     * @brief Recovered clock output pins are rclk0 - 0, rclk1 - 1 and rclk2 - 2
     *
     * @type sai_uint32_t
     * @flags CREATE_AND_SET
     * @default 0
     */
    SAI_PORT_ATTR_SYNCE_RCLK_PIN,


# Configuration Example

Following example shows how to setup Recovered Clock configuration on a port. In this example a 16 lane PHY is used.

    /\* Create System side, Line side, and System Side Failover ports \*/
    sys\_attr[0].value.u32list.list = sys\_lane\_list;
    line\_attr[0].value.u32list.list = line\_lane\_list;
    failover\_attr[0].value.u32list.list = failover\_lane\_list;
    line\_attr[1].id = sys\_attr[1].id = SAI\_PORT\_ATTR\_SPEED;
    line\_attr[1].value.u32= sys\_attr[1].value.u32 = 100000;
    line\_attr[2].id = sys\_attr[2].id = SAI\_PORT\_ATTR\_INTERFACE\_TYPE;
    line\_attr[2].value.u32 = sys\_attr[2].value.u32 = SAI\_PORT\_INTERFACE\_TYPE\_KR;
    line\_attr[3].id = sys\_attr[3].id = SAI\_PORT\_ATTR\_FEC\_MODE;
    line\_attr[3].value.u32 = sys\_attr[3].value.u32 = SAI\_PORT\_FEC\_MODE\_RS;
    line\_attr[4].id = sys\_attr[4].id = SAI\_PORT\_ATTR\_LINK\_TRAINING\_ENABLE;
    line\_attr[4].value.booldata = sys\_attr[4].value.booldata = 1;
    line\_attr[5].id = sys\_attr[5].id = SAI\_PORT\_ATTR\_ADMIN\_STATE;
    line\_attr[5].value.booldata = sys\_attr[5].value.booldata = 1;
    line\_attr[6].id = SAI\_PORT\_ATTR\_SYNCE\_GEN\_SQUELCH\_CONFIG;
    line\_attr[6].value.u32 = 1;
    line\_attr[7].id = SAI\_PORT\_ATTR\_SYNCE\_CLOCK\_OUTPUT\_LANE;
    line\_attr[7].value.u32 = 21;
    line\_attr[8].id = SAI\_PORT\_ATTR\_SYNCE\_DIVIDER;
    line\_attr[8].value.u32 = SAI\_PORT\_SYNCE\_DIVIDER\_1024;
    line\_attr[9].id = SAI\_PORT\_ATTR\_SYNCE\_RCLK\_PIN;
    line\_attr[9].value.u32 = 0;
    for (port\_index = 0; port\_index \&lt; 1; port\_index ++) {
        for (phy\_index = 0; phy\_index \&lt; PAI\_MAX\_PHY; phy\_index ++) {
            attr\_count = 1;
            memset(&amp;port\_attr\_get, 0, sizeof(port\_attr\_get));
            port\_attr\_get[0].id = SAI\_PORT\_ATTR\_SYNCE\_GEN\_SQUELCH\_CONFIG;
            rv = pai\_port\_apis\_ptr-\&gt;get\_port\_attribute(line\_port\_id[phy\_index][port\_index], attr\_count, port\_attr\_get);
            if (SAI\_STATUS\_SUCCESS != rv) {
                printf(&quot;get Port Attribute failed return:%d\n&quot;, rv);
                return rv;
            }
            printf(&quot;PAI Port synce config get attribute values port\_attr\_get[%d].id:%d\n&quot;, phy\_index, port\_attr\_get[0].value.u32);
        }
    }

    for (port\_index = 0; port\_index \&lt; 1; port\_index ++) {
        for (phy\_index = 0; phy\_index \&lt; PAI\_MAX\_PHY; phy\_index ++) {
            attr\_count = 1;
            memset(&amp;port\_attr\_get, 0, sizeof(port\_attr\_get));
            port\_attr\_get[0].id = SAI\_PORT\_ATTR\_SYNCE\_CLOCK\_OUTPUT\_LANE;
            rv = pai\_port\_apis\_ptr-\&gt;get\_port\_attribute(line\_port\_id[phy\_index][port\_index], attr\_count, port\_attr\_get);
            if (SAI\_STATUS\_SUCCESS != rv) {
                printf(&quot;get Port Attribute failed return:%d\n&quot;, rv);
                return rv;
            }
            printf(&quot;PAI Port synce config get attribute values port\_attr\_get[%d].id:%d\n&quot;, phy\_index, port\_attr\_get[0].value.u32);
        }
    }

    for (port\_index = 0; port\_index \&lt; 1; port\_index ++) {
        for (phy\_index = 0; phy\_index \&lt; PAI\_MAX\_PHY; phy\_index ++) {
            port\_attr\_set.id = SAI\_PORT\_ATTR\_SYNCE\_GEN\_SQUELCH\_CONFIG;
            port\_attr\_set.value.u32 = 0;
            printf(&quot;PAI Port synce mode attribute values :%d\n&quot;, port\_attr\_set.value.u32);
            rv = pai\_port\_apis\_ptr-\&gt;set\_port\_attribute(line\_port\_id[phy\_index][port\_index], &amp;port\_attr\_set);
            if (SAI\_STATUS\_SUCCESS != rv) {
                printf(&quot;Set Port Attribute failed return:%d\n&quot;, rv);
                return rv;
            }
            port\_attr\_set.id = SAI\_PORT\_ATTR\_SYNCE\_RCLK\_PIN;
            port\_attr\_set.value.u32 = 2;
            printf(&quot;PAI Port synce mode attribute values :%d\n&quot;, port\_attr\_set.value.u32);
            rv = pai\_port\_apis\_ptr-\&gt;set\_port\_attribute(line\_port\_id[phy\_index][port\_index], &amp;port\_attr\_set);
            if (SAI\_STATUS\_SUCCESS != rv) {
                printf(&quot;Set Port Attribute failed return:%d\n&quot;, rv);
                return rv;
            }
            port\_attr\_set.id = SAI\_PORT\_ATTR\_SYNCE\_CLOCK\_OUTPUT\_LANE;
            port\_attr\_set.value.u32 = 3;
            printf(&quot;PAI Port synce mode attribute values :%d\n&quot;, port\_attr\_set.value.u32);
            rv = pai\_port\_apis\_ptr-\&gt;set\_port\_attribute(line\_port\_id[phy\_index][port\_index], &amp;port\_attr\_set);
            if (SAI\_STATUS\_SUCCESS != rv) {
                printf(&quot;Set Port Attribute failed return:%d\n&quot;, rv);
                return rv;
            }
        }
    }

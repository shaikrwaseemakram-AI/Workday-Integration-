1. Core Connector Worker (CCW) – Sample XML

File: connectors/ccw_example.xml

<?xml version="1.0" encoding="UTF-8"?>
<wd:Report_Data xmlns:wd="urn:com.workday/bsvc">
  <wd:Worker>
    <wd:Worker_ID>12345</wd:Worker_ID>
    <wd:Name>
      <wd:First_Name>John</wd:First_Name>
      <wd:Last_Name>Doe</wd:Last_Name>
    </wd:Name>
    <wd:Position>
      <wd:Position_ID>9876</wd:Position_ID>
      <wd:Title>Software Developer</wd:Title>
      <wd:Supervisory_Org>IT Department</wd:Supervisory_Org>
    </wd:Position>
    <wd:Contact>
      <wd:Email>john.doe@example.com</wd:Email>
      <wd:Phone>+1-555-123-4567</wd:Phone>
    </wd:Contact>
  </wd:Worker>
</wd:Report_Data>


✅ This simulates a Core Connector Worker (CCW) outbound XML payload.

2. XSLT Transformation – XML → CSV

File: transformations/xslt_samples/xml_to_csv.xslt

<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="2.0" 
  xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

  <xsl:output method="text" encoding="UTF-8"/>

  <!-- CSV Header -->
  <xsl:template match="/">
    <xsl:text>Worker_ID,First_Name,Last_Name,Email,Phone&#10;</xsl:text>
    <xsl:apply-templates select="//wd:Worker"/>
  </xsl:template>

  <!-- Worker Row -->
  <xsl:template match="wd:Worker" xmlns:wd="urn:com.workday/bsvc">
    <xsl:value-of select="wd:Worker_ID"/><xsl:text>,</xsl:text>
    <xsl:value-of select="wd:Name/wd:First_Name"/><xsl:text>,</xsl:text>
    <xsl:value-of select="wd:Name/wd:Last_Name"/><xsl:text>,</xsl:text>
    <xsl:value-of select="wd:Contact/wd:Email"/><xsl:text>,</xsl:text>
    <xsl:value-of select="wd:Contact/wd:Phone"/><xsl:text>&#10;</xsl:text>
  </xsl:template>
</xsl:stylesheet>


✅ This transforms the CCW XML into a CSV file for downstream systems.

3. EIB Outbound Integration – Template XML

File: connectors/eib_outbound_template.xml

<?xml version="1.0" encoding="UTF-8"?>
<wd:Report_Data xmlns:wd="urn:com.workday/bsvc">
  <wd:Workers>
    <wd:Worker>
      <wd:Worker_ID>001</wd:Worker_ID>
      <wd:Name>
        <wd:First_Name>Alice</wd:First_Name>
        <wd:Last_Name>Smith</wd:Last_Name>
      </wd:Name>
      <wd:Email>alice.smith@example.com</wd:Email>
      <wd:Hire_Date>2022-06-01</wd:Hire_Date>
    </wd:Worker>
    <wd:Worker>
      <wd:Worker_ID>002</wd:Worker_ID>
      <wd:Name>
        <wd:First_Name>Bob</wd:First_Name>
        <wd:Last_Name>Johnson</wd:Last_Name>
      </wd:Name>
      <wd:Email>bob.johnson@example.com</wd:Email>
      <wd:Hire_Date>2023-01-15</wd:Hire_Date>
    </wd:Worker>
  </wd:Workers>
</wd:Report_Data>


✅ This represents a Workday EIB Outbound pulling worker data for an external system.# Workday-Integration-

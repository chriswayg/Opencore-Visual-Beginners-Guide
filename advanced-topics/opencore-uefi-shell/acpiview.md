---
description: Display ACPI Table information.
---

# acpiview - command

```
Display ACPI Table information.
 
ACPIVIEW [[-?] | [[[[-l] | [-s AcpiTable [-d]]] [-q] [-h]] [-r Spec]]]
 
 
  -l - Display list of installed ACPI Tables.
  -s - Display only the specified AcpiTable type and only support single
       invocation option.
         AcpiTable    : The required ACPI Table type.
  -d - Generate a binary file dump of the specified AcpiTable.
  -q - Quiet. Suppress errors and warnings. Disables consistency checks.
  -h - Enable colour highlighting.
  -r - Validate that all required ACPI tables are installed
         Spec  : Specification to validate against.
                 For Arm, the possible values are:
                   0 - Server Base Boot Requirements v1.0
                   1 - Server Base Boot Requirements v1.1
                   2 - Server Base Boot Requirements v1.2
  -? - Show help.
 
 
  This program is provided to allow examination of ACPI table values from the
  UEFI Shell.  This can help with investigations, especially at that stage
  where the tables are not enabling an OS to boot.
  The program is not exhaustive, and only encapsulates detailed knowledge of a
  limited number of table types.
 
  Default behaviour is to display the content of all tables installed.
  'Known' table types (listed in NOTES below) will be parsed and displayed
  with descriptions and field values.  Where appropriate a degree of
  consistency checking is done and errors may be reported in the output.
  Other table types will be displayed as an array of Hexadecimal bytes.
 
  To facilitate debugging, the -s and -d options can be used to generate a
  binary file image of a table that can be copied elsewhere for investigation
  using tools such as those provided by acpica.org.  This is especially
  relevant for AML type tables like DSDT and SSDT.
 
NOTES:
  1. The AcpiTable parameter can match any installed table type.
     Tables without specific handling will be displayed as a raw hex dump (or
     dumped to a file if -d is used).
  2. -s option supports to display the specified AcpiTable type that is present
     in the system. For normal type AcpiTable, it would display the data of the
     AcpiTable and AcpiTable header. The following type may contain header type
     other than AcpiTable header. The actual header can refer to the ACPI spec
     6.2
     Extra A. Particular types:
       AEST  - Arm Error Source Table
       APIC  - Multiple APIC Description Table (MADT)
       BGRT  - Boot Graphics Resource Table
       DBG2  - Debug Port Table 2
       DSDT  - Differentiated System Description Table
       FACP  - Fixed ACPI Description Table (FADT)
       GTDT  - Generic Timer Description Table
       HMAT  - Heterogeneous Memory Attributes Table
       IORT  - IO Remapping Table
       MCFG  - Memory Mapped Config Space Base Address Description Table
       PPTT  - Processor Properties Topology Table
       RSDP  - Root System Description Pointer
       SLIT  - System Locality Information Table
       SPCR  - Serial Port Console Redirection Table
       SRAT  - System Resource Affinity Table
       SSDT  - Secondary SystemDescription Table
       XSDT  - Extended System Description Table
 
 
 
EXAMPLES:
  * To display a list of the installed table types:
    fs0:\> acpiview -l
 
  * To parse and display a specific table type:
    fs0:\> acpiview -s GTDT
 
  * To save a binary dump of the contents of a table to a file
    in the current working directory:
    fs0:\> acpiview -s DSDT -d
 
  * To display contents of all ACPI tables:
    fs0:\> acpiview
 
  * To check if all Server Base Boot Requirements (SBBR) v1.2 mandatory
    ACPI tables are installed (Arm only):
    fs0:\> acpiview -r 2

```

See also: [ARM adds ACPIView tool to UEFI Shell: dump ACPI tables – Firmware Security](https://firmwaresecurity.com/2017/12/15/arm-adds-acpiview-tool-to-uefi-shell-dump-acpi-tables/)

![](../../.gitbook/assets/by-nc-license.png) _Except where otherwise noted, content on this site is licensed under the_ [_Creative Commons — Attribution-NonCommercial 4.0 International — CC BY-NC 4.0_](https://creativecommons.org/licenses/by-nc/4.0/) _license. Attribution by link to_ [_chriswayg · GitHub_](https://github.com/chriswayg)_._

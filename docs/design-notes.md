# Design notes — USB-C 5V Input & Protection Board

## Assumptions

CC1 and CC2 are each fitted with 5.1 kOhm Rd resistors to advertise a sink. VBUS is fused before the TVS/LDO path. The board is not a USB data interface.

Component selection uses manufacturer datasheets linked in the root README. MPN availability should be rechecked at purchasing time. No continuous-current guarantee is made without a thermal calculation and measurement.

## Review gates

- Confirm every symbol pin number against the manufacturer datasheet.
- Confirm package land patterns against the latest recommended land pattern.
- Confirm creepage, clearance, copper widths and connector ratings.
- Run KiCad ERC/DRC after assigning project-specific rules.
- Export fresh Gerbers from the reviewed KiCad PCB rather than relying on the preliminary files.

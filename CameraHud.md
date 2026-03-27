# 

# Click anywhere in the box to select all, then copy

# \# Camera Server Node — Build Plan \& Parts List

# 

# \## Overview

# Three to four U server node for a camera control system. Covers

# external/interior cameras via PyCam integration plus 10–12 dedicated

# pool table cameras for data recording and analytics. Remote access via

# Cloudflare Tunnel.

# 

# \---

# 

# \## Cameras

# 

# \### Fixed (Pool Tables) — 4K

# | Model | Notes |

# |---|---|

# | Hikvision DS-2CD2143G2-I | Solid 4K, reliable, good value |

# | Axis M3045-WV | Industrial-grade, excellent build |

# | Uniview IPC322SR-DVS28 | Budget-friendly, strong 4K |

# 

# \### Pan-Tilt-Zoom (Optional)

# | Model | Notes |

# |---|---|

# | Hikvision DS-2DE4425IW-DE | 4K PTZ, strong movement range |

# 

# \---

# 

# \## Networking

# 

# \### Switches (\~$200, 20–40 cameras)

# | Model | Ports | Notes |

# |---|---|---|

# | Netgear GS728T | 28 | Managed gigabit, VLAN + QoS |

# | Ubiquiti EdgeSwitch 24 | 24 | Solid throughput, clean UI |

# 

# \### Firewall

# | Model | Notes |

# |---|---|

# | Ubiquiti Dream Machine | All-in-one, easy management |

# | Firewalla Gold | Lightweight, privacy-focused |

# 

# > Remote access: Cloudflare Tunnel (no exposed ports)

# 

# \---

# 

# \## Server Build

# 

# > Option: Pre-built mini PC (\~$500) as alternative to custom ATX build.

# > An i5 is sufficient — no need to overspend on compute for this workload.

# 

# \### Chassis (ATX / Mini ITX)

# | Option | Notes |

# |---|---|

# | Fractal Design Node 804 | Compact, good airflow |

# | Corsair Carbide 270R | Solid budget ATX |

# 

# \### Motherboard

# | Option | Notes |

# |---|---|

# | ASUS ProArt B760-Creator | LGA1700, plenty of expansion |

# | MSI B760-A Pro | Reliable, budget-friendly |

# 

# \### CPU

# | Model | Base | Boost |

# |---|---|---|

# | Intel Core i5-12400F | 3.4 GHz | 4.4 GHz |

# 

# \### RAM

# | Model | Spec |

# |---|---|

# | Corsair Vengeance LPX | 16GB DDR4-3200 |

# 

# \### Power Supply

# | Option | Wattage |

# |---|---|

# | Corsair RM750x | 750W |

# | EVGA SuperNOVA 750 G6 | 750W |

# 

# \---

# 

# \## Storage

# 

# | Drive | Purpose | Size | Est. Cost |

# |---|---|---|---|

# | Samsung 970 EVO Plus / Crucial P5 Plus | OS boot (SSD) | 512GB | \~$60 |

# | Samsung 870 QVO / WD Red Pro | Local daily buffer (on-site) | 1TB | \~$80 |

# | NAS Drive (off-site grid array) | 3-day archive | 16TB | \~$500 |

# 

# \### Storage Estimate

# \- 40 cameras × 4K × 3 days ≈ 6–9TB minimum

# \- \*\*16TB recommended\*\* for the off-site NAS

# 

# \---

# 

# \## Game Plan

# 

# 1\. Deploy 10–12 fixed 4K cameras over pool tables (PTZ option available)

# 2\. Run all cameras through managed gigabit switch

# 3\. Server node handles local 1TB daily buffer, syncs to off-site 16TB NAS

# 4\. Firewall secures the network; Cloudflare Tunnel handles remote access

# 5\. PyCam integration for external and interior camera system

# 6\. Data recording and analytics pipeline built on top of camera feeds

# 

# \---

# 

# \*Build workshopped with Claude — parts subject to availability and pricing at time of purchase.\*


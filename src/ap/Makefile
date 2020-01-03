all: libap.a

clean:
	rm -f *~ *.o *.d *.gcno *.gcda *.gcov libap.a

install:
	@echo Nothing to be made.

include ../lib.rules

CFLAGS += -DHOSTAPD
CFLAGS += -DNEED_AP_MLME
CFLAGS += -DCONFIG_HS20
CFLAGS += -DCONFIG_INTERWORKING
CFLAGS += -DCONFIG_IEEE80211R
CFLAGS += -DCONFIG_IEEE80211R_AP
CFLAGS += -DCONFIG_WPS
CFLAGS += -DCONFIG_PROXYARP
CFLAGS += -DCONFIG_IPV6

LIB_OBJS= \
	ap_config.o \
	ap_drv_ops.o \
	ap_list.o \
	ap_mlme.o \
	authsrv.o \
	beacon.o \
	bss_load.o \
	dfs.o \
	dhcp_snoop.o \
	drv_callbacks.o \
	eap_user_db.o \
	gas_serv.o \
	hostapd.o \
	hs20.o \
	hw_features.o \
	ieee802_11_auth.o \
	ieee802_11.o \
	ieee802_11_ht.o \
	ieee802_11_shared.o \
	ieee802_11_vht.o \
	ieee802_1x.o \
	neighbor_db.o \
	ndisc_snoop.o \
	pmksa_cache_auth.o \
	preauth_auth.o \
	rrm.o \
	sta_info.o \
	tkip_countermeasures.o \
	utils.o \
	wmm.o \
	wnm_ap.o \
	wpa_auth.o \
	wpa_auth_glue.o \
	wpa_auth_ie.o \
	wps_hostapd.o \
	x_snoop.o

ifndef CONFIG_NO_ACCOUNTING
LIB_OBJS+=	accounting.o
endif

ifndef CONFIG_NO_VLAN
LIB_OBJS+= \
	vlan.o \
	vlan_ifconfig.o \
	vlan_init.o
ifdef CONFIG_FULL_DYNAMIC_VLAN
LIB_OBJS+= vlan_full.o
ifdef CONFIG_VLAN_NETLINK
LIB_OBJS+= vlan_util.o
else
LIB_OBJS+= vlan_ioctl.o
endif
endif
endif

ifdef CONFIG_TAXONOMY
LIB_OBJS+= taxonomy.o
endif

ifndef CONFIG_NO_CTRL_IFACE
LIB_OBJS+= ctrl_iface_ap.o
endif

ifdef CONFIG_IEEE80211R
LIB_OBJS+= wpa_auth_ft.o
endif

ifdef NEED_ETH_P_OUI
LIB_OBJS+= eth_p_oui.o
endif

ifdef CONFIG_AIRTIME_POLICY
LIB_OBJS+= airtime_policy.o
endif

ifdef CONFIG_FILS
LIB_OBJS+= fils_hlp.o
endif

# XXX TODO: CONFIG_WNM_AP is set for AP builds and wpa_supplicant
# builds with CONFIG_AP enabled.  Should check with jouni if these
# bits need to be run-time configured via a global or something.
ifdef CONFIG_WNM
LIB_OBJS+= wnm_ap.o
endif

ifdef CONFIG_IEEE80211AX
LIB_OBJS+= ieee802_11_he.o
endif

ifdef CONFIG_MBO
LIB_OBJS+= mbo_ap.o
endif

ifdef CONFIG_WPS
LIB_OBJS+= wps_hostapd.o
endif

ifdef CONFIG_DPP
LIB_OBJS+= \
	dpp_hostapd.o \
	gas_query_ap.o
endif

ifdef CONFIG_MACSEC
LIB_OBJS+= wpa_auth_key.o
endif

ifdef NEED_AP_MLME
LIB_OBJS += \
	wmm.o \
	ap_list.o \
	ieee802_11.o \
	hw_features.o \
	dfs.o
endif

ifdef CONFIG_IEEE80211N
LIB_OBJS+= ieee8021_11_ht.o
endif

ifdef CONFIG_IEEE80211AC
LIB_OBJS+= ieee802_11_vht.o
endif

# XXX TODO: Note: this also needs to be added if CONFIG_P2P is enabled
ifdef CONFIG_P2P_MANAGER
LIB_OBJS+= p2p_hostapd.o
endif

ifdef CONFIG_HS20
LIB_OBJS+= hs20.o
endif

libap.a: $(LIB_OBJS)
	$(AR) crT $@ $?

-include $(OBJS:%.o=%.d)


noinst_LTLIBRARIES = \
	libconfig_parser.la
libconfig_parser_la_SOURCES =
BUILT_SOURCES =

AM_LFLAGS = -Plibvma_yy
AM_YFLAGS = -plibvma_yy -d
LEX_OUTPUT_ROOT=lex.libvma_yy

# consider config_scanner.c, config_parser.c, config_parser.h as source (and not
# as built) because we don't want it to be created by old version of flex/yacc
# on some machines that will generate gcc warmings.
# in case you change the *.l or *.y in the future - than change the commenting in the following 3 lines
#-----
#BUILT_SOURCES += config_scanner.c config_parser.h config_parser.c
#libconfig_parser_la_SOURCES += util/config_scanner.l util/config_parser.y
libconfig_parser_la_SOURCES += config_scanner.c config_parser.c


CLEANFILES = $(BUILT_SOURCES)
dist-hook:
	cd $(distdir); rm -f $(BUILT_SOURCES)

SUBDIRS = infra netlink

EXTRA_DIST = \
	util/hash_map.inl \
	util/libvma.conf \
	util/30-libvma-limits.conf

sysconf_DATA = util/libvma.conf
othersysconfdir=$(sysconfdir)/security/limits.d
othersysconf_DATA=util/30-libvma-limits.conf
otherincludedir = $(includedir)/mellanox
otherinclude_HEADERS = vma_extra.h

install-exec-hook:
	rm -f $(DESTDIR)$(libdir)/libvma.la
	rm -f $(DESTDIR)$(libdir)/libvma.a
	rm -f $(DESTDIR)$(bindir)/state_machine_test
	rm -f $(DESTDIR)$(bindir)/vlogger_test
	if [[ `id -u` -eq 0 ]];then /sbin/ldconfig || true;fi

uninstall-hook:
	rm -f $(DESTDIR)$(libdir)/libvma.so*

lib_LTLIBRARIES = libvma.la

AM_CPPFLAGS := \
	-I$(top_srcdir)/src ${LIBNL_CFLAGS}

if IS_RELEASE_ZERO
libvma_la_LDFLAGS := -no-undefined -version-number @VMA_LIBRARY_MAJOR@:@VMA_LIBRARY_MINOR@:@VMA_LIBRARY_REVISION@ 
else
libvma_la_LDFLAGS := -no-undefined -version-number @VMA_LIBRARY_MAJOR@:@VMA_LIBRARY_MINOR@:@VMA_LIBRARY_REVISION@ -release @VMA_LIBRARY_RELEASE@
endif

libvma_la_LIBADD = \
	-lrt -ldl -lpthread -libverbs -lrdmacm $(LIBNL_LIBS) \
	$(top_builddir)/src/utils/libutils.la \
	$(top_builddir)/src/vlogger/libvlogger.la \
	$(top_builddir)/src/state_machine/libstate_machine.la \
	$(top_builddir)/src/stats/libstats.la \
	$(top_builddir)/src/vma/netlink/libnetlink.la \
	$(top_builddir)/src/vma/infra/libinfra.la \
	libconfig_parser.la
	
libvma_la_SOURCES := \
	dev/ah_cleaner.cpp \
	dev/buffer_pool.cpp \
	dev/cq_mgr.cpp \
	dev/qp_mgr.cpp \
	dev/gro_mgr.cpp \
	dev/ring_allocation_logic.cpp \
	dev/rfs.cpp \
	dev/rfs_uc.cpp \
	dev/rfs_uc_tcp_gro.cpp \
	dev/rfs_mc.cpp \
	dev/ib_ctx_time_converter.cpp \
	dev/ib_ctx_handler.cpp \
	dev/ib_ctx_handler_collection.cpp \
	dev/net_device_val.cpp \
	dev/net_device_entry.cpp \
	dev/net_device_table_mgr.cpp \
	dev/wqe_send_handler.cpp \
	dev/wqe_send_ib_handler.cpp \
	dev/ring.cpp \
	dev/ring_simple.cpp \
	dev/ring_bond.cpp \
	\
	event/delta_timer.cpp \
	event/event_handler_manager.cpp \
	event/vlogger_timer_handler.cpp \
	event/netlink_event.cpp \
	event/route_net_dev_event.cpp\
	\
	iomux/epfd_info.cpp \
	iomux/epoll_wait_call.cpp \
	iomux/io_mux_call.cpp \
	iomux/poll_call.cpp \
	iomux/select_call.cpp \
	\
	lwip/pbuf.c \
	lwip/tcp.c \
	lwip/tcp_in.c \
	lwip/tcp_out.c \
	lwip/cc.c \
	lwip/cc_lwip.c \
	lwip/cc_cubic.c \
	lwip/init.c \
	\
	proto/ip_frag.cpp \
	proto/flow_tuple.cpp \
	proto/vma_lwip.cpp \
	proto/neighbour.cpp \
	proto/neighbour_table_mgr.cpp \
	proto/L2_address.cpp \
	proto/route_table_mgr.cpp \
	proto/route_entry.cpp \
	proto/route_val.cpp \
	proto/rule_table_mgr.cpp \
	proto/rule_entry.cpp \
	proto/rule_val.cpp \
	proto/dst_entry.cpp \
	proto/dst_entry_udp.cpp \
	proto/dst_entry_udp_mc.cpp \
	proto/dst_entry_tcp.cpp \
	proto/header.cpp \
	proto/arp.cpp \
	proto/igmp_mgr.cpp \
	proto/igmp_handler.cpp \
	\
	sock/sockinfo.cpp \
	sock/sockinfo_udp.cpp \
	sock/sockinfo_tcp.cpp \
	sock/fd_collection.cpp \
	sock/pipeinfo.cpp \
	sock/socket_fd_api.cpp \
	sock/sock-redirect.cpp \
	\
	util/wakeup.cpp \
	util/wakeup_pipe.cpp \
	util/match.cpp \
	util/utils.cpp \
	util/verbs_extra.cpp \
	util/instrumentation.cpp \
	util/sys_vars.cpp \
	libvma.c \
	main.cpp \
	\
	dev/ah_cleaner.h \
	dev/buffer_pool.h \
	dev/cq_mgr.h \
	dev/gro_mgr.h \
	dev/ib_ctx_handler_collection.h \
	dev/ib_ctx_handler.h \
	dev/ib_ctx_time_converter.h \
	dev/net_device_entry.h \
	dev/net_device_table_mgr.h \
	dev/net_device_val.h \
	dev/qp_mgr.h \
	dev/rfs.h \
	dev/rfs_mc.h \
	dev/rfs_uc.h \
	dev/rfs_uc_tcp_gro.h \
	dev/ring_allocation_logic.h \
	dev/ring_bond.h \
	dev/ring.h \
	dev/ring_simple.h \
	dev/wqe_send_handler.h \
	dev/wqe_send_ib_handler.h \
	event/command.h \
	event/delta_timer.h \
	event/event.h \
	event/event_handler_ibverbs.h \
	event/event_handler_manager.h \
	event/event_handler_rdma_cm.h \
	event/netlink_event.h \
	event/route_net_dev_event.h \
	event/timer_handler.h \
	event/timers_group.h \
	event/vlogger_timer_handler.h \
	infra/sender.h \
	infra/sender_info_dst.h \
	infra/subject_observer.h \
	infra/cache_subject_observer.h \
	iomux/epfd_info.h \
	iomux/epoll_wait_call.h \
	iomux/io_mux_call.h \
	iomux/poll_call.h \
	iomux/select_call.h \
	lwip/cc_cubic.h \
	lwip/cc.h \
	lwip/def.h \
	lwip/err.h \
	lwip/init.h \
	lwip/ip_addr.h \
	lwip/ip.h \
	lwip/opt.h \
	lwip/pbuf.h \
	lwip/stats.h \
	lwip/tcp.h \
	lwip/tcp_impl.h \
	netlink/link_info.h \
	netlink/neigh_info.h \
	netlink/netlink_compatibility.h \
	netlink/netlink_wrapper.h \
	netlink/route_info.h \
	proto/arp.h \
        proto/dst_entry.h \
        proto/dst_entry_tcp.h \
        proto/dst_entry_udp.h \
        proto/dst_entry_udp_mc.h \
        proto/flow_tuple.h \
        proto/header.h \
        proto/igmp_handler.h \
        proto/igmp_mgr.h \
        proto/ip_address.h \
        proto/ip_frag.h \
        proto/L2_address.h \
	proto/mem_buf_desc.h \
	proto/neighbour.h \
	proto/neighbour_observer.h \
	proto/neighbour_table_mgr.h \
	proto/netlink_socket_mgr.h \
	proto/peer_key.h \
	proto/route_entry.h \
	proto/route_rule_table_key.h \
	proto/route_table_mgr.h \
	proto/route_val.h \
	proto/rule_entry.h \
	proto/rule_table_mgr.h \
	proto/rule_val.h \
	proto/vma_lwip.h \
	sock/cleanable_obj.h \
        sock/fd_collection.h \
        sock/pipeinfo.h \
        sock/pkt_rcvr_sink.h \
        sock/pkt_sndr_source.h \
        sock/socket_fd_api.h \
        sock/sockinfo.h \
        sock/sockinfo_tcp.h \
        sock/sockinfo_udp.h \
        sock/sock-redirect.h \
        util/hash_map.h \
        util/if.h \
        util/instrumentation.h \
        util/libvma.h \
        util/linked_unordered_map.h \
        util/list.h \
        util/sock_addr.h \
        util/sysctl_reader.h \
        util/sys_vars.h \
        util/to_str.h \
        util/utils.h \
        util/valgrind.h \
        util/verbs_extra.h \
        util/vma_list.h \
        util/vma_stats.h \
        util/vtypes.h \
        util/wakeup.h \
        util/wakeup_pipe.h \
	config_parser.h \
	main.h \
	vma_extra.h

libvma_la_DEPENDENCIES = \
	$(top_builddir)/src/vlogger/libvlogger.la \
	$(top_builddir)/src/state_machine/libstate_machine.la \
	$(top_builddir)/src/stats/libstats.la \
	$(top_builddir)/src/vma/netlink/libnetlink.la \
	$(top_builddir)/src/vma/infra/libinfra.la \
	libconfig_parser.la


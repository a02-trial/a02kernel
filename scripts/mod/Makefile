# SPDX-License-Identifier: GPL-2.0
OBJECT_FILES_NON_STANDARD := y
CFLAGS_empty.c += $(DISABLE_LTO)

hostprogs-y	:= modpost mk_elfconfig
always		:= $(hostprogs-y) empty.c

modpost-objs	:= modpost.c file2alias.c sumversion.c

devicetable-offsets-file := devicetable-offsets.c

$(obj)/$(devicetable-offsets-file): $(obj)/devicetable-offsets.c FORCE
	$(call filechk,offsets,__DEVICETABLE_OFFSETS_C__)

targets += $(devicetable-offsets-file) devicetable-offsets.c

# dependencies on generated files need to be listed explicitly

$(obj)/modpost.c $(obj)/file2alias.c $(obj)/sumversion.c: $(obj)/mk_elfconfig.c
$(obj)/file2alias.c: $(obj)/$(devicetable-offsets-file)

quiet_cmd_elfconfig = MKELF   $@
      cmd_elfconfig = $(obj)/mk_elfconfig < $< > $@

$(obj)/mk_elfconfig.c: $(obj)/empty.c $(obj)/mk_elfconfig FORCE
	$(call if_changed,elfconfig)

targets += mk_elfconfig.c

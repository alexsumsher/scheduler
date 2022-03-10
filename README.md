# scheduler
schedule event handler

from Libs import sys_gardD, event

maintain_jobs = [
	event.new_event(event.ETYPE_HOURS, 'do_alerts', act_maintain.alert_reporter, 0.5, runmode=event.RUN_THREAD),
	event.new_event(event.ETYPE_HOURS, 'summary_prj_infos', act_maintain.tabulate_projects, 6.01, runmode=event.RUN_THREAD),
	event.new_event(event.ETYPE_MONTHLY, 'zip-log', act_maintain.monlog_zipper, -1, '01:00:00', runmode=event.RUN_THREAD),
	event.new_event(event.ETYPE_YEARLY, 'yearly_table', act_maintain.yearly_table, "12-31", "23:00:00", runmode=event.RUN_THREAD),
]

maintainer = sys_gardD()

maintainer.add_events(*maintain_jobs)

maintainer.bind_arg('do_alerts', mail_queue)

maintainer.start()

                # MMR(LOB) only: Spot and MX_2 rows share the same OU + account + scenario, so
                # their X keys would collide and the template's INDEX/MATCH would only ever find
                # the first one. Suffix the Spot rows so each measure has a distinct key
                # (the template's lookup key was updated to match: "...Adjusted Actual - Spot").
                # MX_2 rows are left unchanged. The MMFR reports have no reporting_measure on rows.
                if _report_name == "MMR(LOB)":
                    spot_mask = df["reporting_measure"] == "Spot"
                    df.loc[spot_mask, "X"] = df.loc[spot_mask, "X"] + " - Spot"
